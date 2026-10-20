---
title: "Sigma Language"
date: 2025-10-09 13:41:00 +0700
categories: ["TryHackMe", "SOC LV 2", "Detection Engineering"]
tags: ["tryhackme", "detection-engineering"]
description: "Sigma is an open, generic, YAML-based signature format for describing log events in a structured, human-readable way."
media_subpath: /assets/img/tryhackme/2025-10-09-sigma-language/
toc: true
comments: false
hidden: true
permalink: /tryhackme/soc-lv-2/detection-engineering/sigma-language/
th_id: "soc-lv-2/detection-engineering/sigma-language"
th_parent: "soc-lv-2/detection-engineering"
th_kind: note
th_order: 1
th_course: "soc-lv-2"
th_module: "soc-lv-2/detection-engineering"
th_size: 0
th_ancestors: ["soc-lv-2", "soc-lv-2/detection-engineering"]
---

{% include tryhackme-nav.html %}

Sigma is an **open, generic, YAML-based signature format** for describing log events in a structured, human-readable way. 

The cleanest way to think about Sigma is by comparing it with other detection languages:

| **Format** | **Used for** |
| --- | --- |
| **Snort / Suricata rules** | Network traffic |
| **YARA rules** | Files and malware |
| **Sigma rules** | Log events |

**The Problem Sigma Solves**

SPlunk, MS Sentinal,Elastic. Three different query languages. Three different field names. If your SOC migrates from Splunk to Sentinel next quarter, every single one of your detections has to be rewritten by hand. Multiply that across hundreds of rules, and you're looking at months of work.

The pain gets sharper in an MSSP context. If you're working at a managed security provider, you're not running one single SIEM; it's often one **per customer**. Customer A is on Splunk, Customer B is on Sentinel, and Customer C is on Elastic. Without a portable format, every new detection has to be authored, tested, and tuned three times over. Sigma flips the economics: the analyst writes the detection logic once, and the conversion step produces the right query for each customer's stack.

**Where Sigma Fits in the SOC Workflow**

![image.png](image.png)

**The Sigma Ecosystem.**

- **Sigma Rules**: the YAML files themselves. A single rule is a single `.yml` file describing one detection.
- **SigmaHQ Repository**: the public, community-driven ruleset on GitHub at [`SigmaHQ/sigma`(opens in new tab)](https://github.com/SigmaHQ/sigma). Thousands of rules contributed by detection engineers worldwide, curated and reviewed by maintainers.
- **sigma-cli**: the modern converter that reads a Sigma rule and emits a backend query. Very popular in automated .
    
    pipelines
    
- **Uncoder.io**: a free web-based converter from  Prime. Useful for quickly translating a Sigma rule into a SIEM query without installing anything locally.
    
    SOC
    

## 1. Anotomy of a Sigma rule

### a. The YAML skeleton

A Sigma rule is a single YAML file with four logical sections:

- **Metadata**: the `title`, `id`, `status`, `description`, `references`, `author`, `date`, and `tags` keys. It defines who wrote the rule, what it detects, and what it maps to in MITRE ATT&CK.
    - status : Lifecycle stage: `experimental`, `test`, `stable`, or `deprecated`.
- **Log Source**: the `logsource` block. It defines what kind of data the rule applies to.
    - category : the type of log event. Examples: `process_creation`, `network_connection` ,…
    - product :  the vendor or platform. Examples: `windows`, `linux`, `aws`, `okta`
    - service : the specific service within the product. Examples: `sysmon`, `security`, `powershell`
- **Detection**: the `detection` block. It defines the actual logic that decides whether an event matches.
    - selections : is a named block of field/value pairs that need to match. The name is up to you, for example: `selection`, `selection_img`, `filter_admin`, `keywords`, anything descriptive. The convention is to prefix exclusions with `filter_` and inclusions with `selection_`, but the names themselves carry no special meaning. They're labels you reference later in the condition. Think that a selection is like the parentheses `()` in most of the query languages, but with names. All the conditions inside a selection should match.
    - condition: `condition` is a boolean expression that combines selections. The simplest condition is a single selection name. From there, you can use `and`, `or`, `not`, and a few helpers:
    
    | **Condition** | **Meaning** |
    | --- | --- |
    | `selection` | Match if `selection` matches |
    | `selection and not filter_admin` | Match `selection`, except when `filter_admin` also matches |
    | `1 of selection_*` | Match if at least one selection starting with `selection_` matches |
    | `all of selection_*` | All selections starting with `selection_` must match |
    | `all of them` | Every selection in the rule must match |
- **Triage**: the `falsepositives` and `level` keys. It defines how the alert should be handled when it fires.
    - falsepositives: a list of known legitimate triggers. This is what you read first when triaging an alert: "Are any of these known FPs in play?"
    - **level**: the severity: `informational`, `low`, `medium`, `high`, or `critical`. Maps to the alert priority in the SIEM.

```
title: Certutil Download
id: 9a1b2c3d-4e5f-6789-abcd-ef0123456789
status: experimental
description: Detects the use of certutil.exe to download remote files, a common LOLBin technique.
references:
  - https://attack.mitre.org/techniques/T1105/
author: SOC Team
date: 2025/01/15
tags:
  - attack.command_and_control
  - attack.t1105
logsource:
  category: process_creation
  product: windows
detection:
  selection:
    Image|endswith: '\certutil.exe'
    CommandLine|contains: '-urlcache'
  condition: selection
falsepositives:
  - Legitimate certificate operations
level: medium
```

## 2. Writing a Sigma Rule

 In this task, you'll author a Sigma rule from scratch. You'll write a rule that catches multiple recon commands an attacker typically runs in the first few minutes after landing on a Windows host.

```
whoami
whoami /priv
whoami /groups
net user
net user /domain
net group "Domain Admins" /domain
net localgroup Administrators
ipconfig /all
systeminfo
nltest /dclist:tryhatme.thm
```

Your job is to write a single Sigma rule that catches as many of these as possible. 

- Step 1 : filling Metadata : Don't skip this, the metadata is what your future self (or your teammate at 2 AM) reads when this rule fires.

```
title: Windows Recon Commands Detection
id: 17769c90-230e-488b-a463-e05c083kd48c
status: experimental
description: <one or two sentences on what the rule catches and why>
references:
  - https://attack.mitre.org/techniques/T1087/
  - https://attack.mitre.org/techniques/T1082/
  - https://attack.mitre.org/techniques/T1016/
author: TryHackMe User
date: 2026/01/01
tags:
  - attack.discovery
  - attack.t1087
  - attack.t1082
  - attack.t1016
```

- Step 2 : Log Source : what kind of data this rule expects. Consider that you are trying to detect command execution (*which log category is best for this?*), specifically for Windows.
Refer to the official Sigma [log source documentation(opens in new tab)](https://sigmahq.io/docs/basics/log-sources.html) if you are unsure about the options for the log source step.

```
logsource:
  category: #Fill the category
  product: windows

```

- **Step 3 : Selecting Standalone Recon Binaries**

 You want a **single selection** that matches if `Image` ends with **any one of them**.

```
  selection_recon_binaries:
    Image|endswith:
      - '\whoami.exe'
      - '\ipconfig.exe'
      - '\nltest.exe'
      - '\systeminfo.exe'
```

- Step 4 :  **Selecting net.exe with Recon Arguments**

Now the second selection: `net.exe` is benign by itself, but the **arguments** that turn it into recon. So the selection needs to match **two things at once**:

+The image must end with `\net.exe`.

+The command line must contain a recon-related parameter, such as `user`.

```
  selection_net_recon:
    Image|endswith: '\net.exe'
    CommandLine|contains:
      - ' user'
      - ' group'
      - ' localgroup'
```

The leading space in `' user'` isn't decorative. Without it, you'd also match command lines that contain words like `username` or `usergroup` that happen to embed those tokens. The space anchors the match to the start of the argument. (You can also use `|startswith` patterns or regex if you want more control, but `contains` with a leading space is the most common approach.)

- Step 5 : Condition : match if at least one selection whose name starts with `selection_` is true.

```
 condition: 1 of selection_*
```

- Step 6 : Triage Fields : Wrap up with the fields that tell triagers how to handle the alert.

`falsepositives` are genuinely large for this rule: IT admins, helpdesk scripts, login banners, asset inventory tools. All of them run these commands. List the categories you can think of. This is giving the next person who triages an alert a head start on the investigation:

```
falsepositives:  - Legitimate IT administrator activity  - Helpdesk troubleshooting scripts  - Asset inventory and CMDB tools
level: low
```

- Step 7 : Validate the Sigma Structure

Before you ship a Sigma rule, it's nice to validate that you used the Sigma structure objects properly with `sigma-cli`. You can test it inside VSCode by opening the embedded Terminal:

![image.png](image%201.png)

Then 

```
cd Desktop/
sigma check first-detection.yml
```

`sigma check` confirms whether the YAML is well-formed, all required fields are present, and the detection block parses cleanly

## 3. From YAML to SIEM query

![image.png](image%202.png)

- Splunk

```
sigma convert -t splunk -p splunk_cim first-detection.yml
```

- Microsoft Sentinel KQL

```
sigma convert -t kusto -p microsoft_xdr first-detection.yml
```

- Elastic EQL

```
sigma convert -t eql -p ecs_windows first-detection.yml
```

## 4. Sigma Rule Tuning
