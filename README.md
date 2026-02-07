# Reachability-Oriented Defense Model (RODM)

**A practical framework for detecting lateral movement through observational asymmetry**

---

## Overview

Modern security monitoring is overwhelmed by noise.  
Traditional approaches attempt to correlate massive volumes of log events, often resulting in fragmented visibility and delayed detection.

The Reachability-Oriented Defense Model (RODM) proposes a different perspective.  
Rather than tracking individual events, RODM focuses on **reachable destinations derived from the next possible login** within a system.

When attackers perform lateral movement, they must start from an initial foothold and identify the next location they can log into.  
RODM treats these destinations as **deterministic transitions based on login relationships** and observes them in a **tree-like structure originating from the initial attack surface**.  
By doing so, RODM enables early detection of lateral movement without requiring a full redesign of the existing system architecture.

---

## Core Idea

RODM is based on the following observation:

> **Attackers achieve lateral movement by acquiring the next login destination.**

Starting from an initial attack surface, an attacker searches for the next location they can log into.  
Once a successful login is achieved, that location becomes a new foothold, from which the attacker again searches for the next reachable login destination.  
By repeating this process, the attacker eventually reaches critical assets.

Therefore, RODM does not directly track attacker behavior or isolated security events.  
Instead, it monitors **login attempts at reachable login destinations**.

Specifically, RODM observes:

- Whether a login attempt occurs at the next reachable login destination when viewed from the initial attack surface  
- Whether a subsequent login attempt occurs at the next reachable login destination, originating from the previously reached destination  

This observation can be repeated **layer by layer**, up to the tier where critical assets reside.

By iteratively applying this approach, defenders gain a **structurally advantageous position over attackers**—  
an **observational asymmetry** in favor of defense.

---

## Detection Reinforcement

To strengthen detection capability:

- Decoys are deployed at each reachable login destination layer  
- Any outbound traffic originating from a reachable login destination can be isolated and treated as potential C2 communication,  
  since internal systems are not expected to initiate outbound communications under normal operation  

---

## Noise and Vulnerability Reduction

To reduce noise and improve observability, access to internal systems is restricted to a designated jump server.  
By limiting legitimate login paths, RODM reduces benign login attempts and clarifies which login transitions should be considered abnormal.

In addition, efforts are made to ensure that internal systems do not expose critical vulnerabilities.  
This eliminates hidden or unintended attack paths, reducing ambiguity in reachability observation.

---

## Intended Audience

- Security architects  
- Blue team / SOC engineers  
- Incident response practitioners  
- Researchers in network and system security  

---

## Repository Scope

This repository currently provides:

- A detailed description of the Reachability-Oriented Defense Model (RODM)  
- The underlying design principles and threat assumptions  
- A concrete detection approach based on login reachability transitions  
- Practical guidance for applying RODM to existing enterprise environments  

This repository focuses on the **conceptual and architectural aspects of RODM**,  
rather than providing a ready-made software implementation.

---
## Further Reading

For a more narrative explanation of the motivation and background behind RODM,  
see the following Medium article:

-[ Reachability-Oriented Defense Model (RODM)  ](https://medium.com/@rodm.sec/reachability-oriented-defense-model-rodm-78249a3e7f34)

  
## Author

**Hiroshi Ohtani**  
Independent Cybersecurity Researcher

---

## License

License to be determined.
