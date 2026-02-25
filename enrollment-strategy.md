
# Enrollment Strategy

---

## Overview

This document outlines the enrollment and onboarding strategy used to introduce endpoints into the secure access architecture. The primary objective of the enrollment design is to ensure that devices begin their lifecycle in a trusted and manageable state while aligning with identity-first security principles.

Enrollment is not treated as a standalone technical task. Instead, it represents the first stage of establishing device trust, enabling compliance evaluation, policy enforcement, and secure access to Microsoft 365 workloads.

---

## Enrollment Objectives

The enrollment approach was guided by several architectural goals:

* Ensure corporate devices enter management automatically and consistently
* Minimise manual configuration during device setup
* Establish device identity within Microsoft Entra ID early in the lifecycle
* Apply security baselines as soon as possible
* Support scalable onboarding for new and replacement devices

The strategy prioritises repeatability and user simplicity rather than complex provisioning workflows.

---

## Device Lifecycle Entry Point

Within the broader architecture, enrollment represents the transition between an unmanaged device and a trusted corporate endpoint.

The lifecycle typically follows this path:

1. Device preparation and registration
2. Windows Autopilot provisioning
3. Microsoft Intune enrollment
4. Policy and application delivery
5. Compliance evaluation

By embedding enrollment into the early stages of device setup, the architecture ensures that endpoints are never operated outside of management for extended periods.

---

## Windows Autopilot Provisioning

Windows Autopilot serves as the primary onboarding mechanism for corporate-managed endpoints.

The design leverages Autopilot to:

* Simplify initial device setup for users
* Automatically join devices to Microsoft Entra ID
* Trigger enrollment into Microsoft Intune
* Apply baseline configuration during provisioning

Rather than relying on traditional imaging processes, Autopilot enables a cloud-native onboarding model aligned with modern endpoint management practices.

Key design considerations included:

* User-driven provisioning for flexibility
* Minimal setup steps to reduce onboarding friction
* Early policy application to establish a secure baseline

---

## Microsoft Intune Enrollment

Following Autopilot provisioning, devices enroll into Microsoft Intune where management policies and compliance requirements are applied.

Enrollment ensures:

* Device identity is associated with the user
* Configuration profiles and security baselines are delivered
* Compliance evaluation begins immediately
* Update and application deployment workflows are triggered

The design assumes that enrollment is automatic and transparent to the user wherever possible, reducing reliance on manual processes.

---

## Identity Integration

Enrollment plays a critical role in establishing the relationship between the endpoint and Microsoft Entra ID.

During onboarding:

* Devices are registered or joined to Entra ID
* Device objects are created within identity directories
* Conditional Access policies can recognise device trust status

This integration ensures that device identity becomes part of authentication context, enabling policy-driven access decisions later in the lifecycle.

---

## Managed vs Unmanaged Enrollment Paths

The enrollment strategy recognises that not all devices follow the same onboarding journey.

### Corporate-Managed Devices

Corporate devices are provisioned through Autopilot and enrolled automatically into Intune. These devices are expected to meet compliance requirements and participate fully in policy enforcement.

### Personal or Unmanaged Devices

Unmanaged endpoints do not follow the same enrollment process. Instead, they are handled through Conditional Access policies that restrict access levels. This distinction reinforces Zero Trust principles by separating trusted and untrusted device paths.

---

## Security Baseline Application

A critical aspect of enrollment design is the early application of security baselines.

During or immediately after enrollment:

* Configuration profiles establish device settings
* Endpoint security policies are applied
* Update management poli
