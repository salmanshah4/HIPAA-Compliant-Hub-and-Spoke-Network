# HIPAA-Compliant-Hub-and-Spoke-Network

### Key Steps

### Link to Loom

<https://loom.com/share/416e368e1228430cadbf35f7cfdb9682>

**1. Define the HIPAA security requirements the network must satisfy** [0:00](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=0)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/36ce8cef-a9ec-4f8b-99d2-b8a58da59efa" />


- Identify the HIPAA safeguards the environment must support before deployment.
- Confirm the design will address: 
  - Encryption in transit and at rest
  - Audit controls and access logging
  - Automatic logoff
  - Integrity controls
  - Transmission security
- Treat these requirements as mandatory design constraints for every resource and network path.

 

**2. Design the hub-and-spoke architecture around compliance controls** [0:43](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=43)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/93ecd1ca-3c11-411d-80b0-e0ccaa780d3e" />


- Use a hub-and-spoke topology as the foundation for the environment.
- Plan the hub to contain shared security and management services.
- Plan the spokes to isolate workloads by sensitivity and purpose.
- Ensure all inter-spoke traffic is forced through the hub for inspection and logging.

 

**3. Build the hub network and shared security services** [0:43](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=43)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b57a1ad5-a021-4cfe-9dfe-58833a875805" />


- Create the hub virtual network.
- Deploy the following shared services into the hub: 
  - Azure Firewall for traffic inspection and control
  - Azure Bastion for secure administrative access
  - Centralized Log Analytics workspace for audit and security logs
  - Key Vault for secret and key management
- Configure the hub as the central enforcement point for network and security policies.

 

**4. Create Spoke One for clinical workloads containing raw ePHI** [1:02](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=62)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/70951b4e-6d14-4e57-9040-3376ca009164" />


- Create a dedicated spoke virtual network for clinical workloads.
- Place workloads that handle raw ePHI in this spoke only.
- Isolate the spoke from direct internet access.
- Allow outbound traffic only through the firewall.
- Ensure the spoke is encrypted and segmented from other environments.

 

**5. Create Spoke Two for analytics workloads using de-identified data** [1:12](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=72)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0ebff1d5-ee4e-4e0f-9fc7-00286116386c" />


- Create a separate spoke virtual network and resource group for analytics workloads.
- Store only de-identified data in this spoke.
- Prevent direct access to Spoke One.
- Keep the analytics environment logically and administratively separate from the clinical environment.
- Route any required traffic through the hub and firewall.

 

**6. Force all spoke-to-spoke traffic through the firewall** [1:27](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=87)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/57ae4759-6195-4548-b536-c65b54f83898" />


- Configure routing so traffic between spokes cannot bypass the hub.
- Send all inter-spoke traffic through Azure Firewall for inspection and logging.
- Verify the firewall is the only approved path between the spokes.
- Use this control to support auditability, segmentation, and threat detection.

 

**7. Implement access control and administrative safeguards** [1:36](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=96)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/02acaeb1-74fc-4325-a208-3fcdaf3a001d" />


- Apply Microsoft Entra ID role-based access control across all resources.
- Use unique user identification for administrative and operational access.
- Use Azure Bastion for secure admin access instead of exposing public management endpoints.
- Use Key Vault to store and manage secrets securely.
- Ensure automatic logoff and least-privilege access are enforced where possible.

 

**8. Enforce encryption, logging, and endpoint restrictions** [2:20](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=140)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e068d93a-248d-49dc-850f-ef8e516db077" />


- Enable centralized Log Analytics for audit and security visibility.
- Configure soft delete for Key Vault and storage.
- Apply immutable storage policies to audit log storage.
- Enforce TLS 1.2 minimum on all applicable resources.
- Disable public endpoints on all data resources.
- Use Customer Managed Keys stored in Key Vault for encryption where required.

 

**9. Enable threat detection and HIPAA policy monitoring** [2:58](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=178)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6660aaab-3b0b-4825-a211-8ff6ed371512" />


- Turn on Microsoft Defender for Cloud.
- Apply the HIPAA-built-in policy initiative.
- Configure alerts for suspicious activity across all resources.
- Use the policy and alerting layer to continuously monitor compliance drift and security events.

 

**10. Deploy and organize the final resource set** [3:22](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=202)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/44950b25-ee23-4409-a164-d557adb15b70" />


- Confirm the environment includes the three main components: 
  - HIPAA Hub
  - HIPAA Spoke One
  - HIPAA Spoke Two
- Verify each spoke is connected to the hub and governed by its own rules.
- Confirm shared services and security controls are centralized in the hub.

 

**11. Validate routing, segmentation, and logging controls** [3:35](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=215)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/864eb7f3-ff49-4d59-9416-e0aab99717ad" />

- Test that user-defined routes point to the firewall.
- Confirm virtual network peering is connected correctly.
- Verify network security groups block internal inbound traffic where required.
- Verify network security groups block internet inbound traffic.
- Confirm Key Vault public access is disabled.
- Check that firewall logs are being written to the Log Analytics workspace.

 

**12. Document the implementation and preserve the Terraform source** [4:13](https://loom.com/share/416e368e1228430cadbf35f7cfdb9682?t=253)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/def3f00b-66bb-4db6-a028-b20f6b5b29c9" />

- Review the Terraform configuration used to deploy the environment.
- Store the code in GitHub for version control and reuse.
- Keep the main Terraform file and supporting modules organized for future maintenance.
- Document any command errors or corrections encountered during validation so the team can avoid repeat issues.

### Cautionary Notes

- Do not allow public access to data resources that may contain ePHI.
- Do not permit direct spoke-to-spoke communication outside the firewall.
- Do not skip log retention, immutable storage, or soft delete settings for audit-related data.
- Ensure all encryption and TLS requirements are enforced before production use.
- Verify that access control is based on least privilege and unique user identity.
- Any misconfiguration that exposes ePHI or weakens logging may create compliance risk.

### Tips for Efficiency

- Use Terraform to deploy the environment consistently and repeatably.
- Centralize logging early so validation is easier during deployment.
- Reuse the hub for shared services instead of duplicating controls in each spoke.
- Validate routing and NSG rules immediately after deployment to catch issues quickly.
- Keep the Terraform code in GitHub to simplify collaboration, review, and rollback.
- Test firewall logging and Key Vault access settings before onboarding workloads.
