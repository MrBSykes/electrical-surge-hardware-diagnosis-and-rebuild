# electrical-surge-hardware-diagnosis-and-rebuild
Breaking down a power surge that took out my personal PC and how I went through diagnosing the issue and how I rebuilt it back up into a smaller form factor.

Electrical Surge Incident Response & Micro-ATX Rebuild
Analyst: Bryan Sykes Date: August 2026 Classification: Personal Hardware Incident Portfolio Documentation


Overview




Project Title
Electrical Surge Incident Response & Full PC Rebuild
Trigger Event
Thunderstorm-related electrical surge; wall outlet and surge protector failure
Systems Affected
Desktop PC (AM5 / Ryzen 5 9600X / RTX 4080 Super), room electrical circuit
Root Cause Identified
ASUS ROG Strix B850-A Gaming WiFi motherboard, sole failed component
Method
Direct visual inspection + component substitution testing (no assumptions)
Outcome
Root cause isolated with zero unnecessary part replacement; full mATX rebuild completed



1. Electrical Hazard Assessment
A power flash caused total room power loss while powering on the PC. The outlet was inspected directly rather than assuming the surge protector alone absorbed the event.

Breaker for the affected room shut off before any further inspection
Wall outlet found with visible burn/scorch damage on the hot-side contact — confirmed the surge protector was not the only casualty
Damaged surge protector (scorched prong) retired
Outlet replaced before any component was reconnected to that circuit


2. Component Isolation Testing
Each major component was cleared through direct substitution, one variable at a time, rather than guesswork.
2.1 Power Supply
Original DeepCool 1000W PSU delivered standby power but system still failed to POST
Swapped in a second, brand-new PSU as a control — identical failure persisted → PSU cleared
Control unit returned for full refund
2.2 Graphics Card
Primary GPU (PNY RTX 4080 Super) reseated; 12VHPWR connector inspected — no pin damage
Second known-good GPU substituted into the same slot — identical failure occurred → both GPUs cleared
2.3 Memory
T-Force Delta DDR5 RGB kit visually inspected — contacts clean, no damage
Barebones boot test (1 stick, no GPU, no drives) still failed → RAM cleared
2.4 Storage
All 4 SSDs pulled and verified individually via external enclosure on a separate laptop
All 4 drives confirmed healthy and readable → zero data loss, storage cleared
2.5 CPU & Socket
CPU contact pads inspected under multiple lighting angles — no scorching or corrosion
Full barebones test (CPU + 1 RAM stick, no GPU, no drives) still failed to POST
With no spare AM5 board/CPU available for cross-testing, a replacement motherboard became the only remaining way to isolate CPU vs. motherboard


3. Root Cause Confirmation
A new ASUS ROG Strix B850-A Gaming WiFi motherboard was installed with the original CPU, RAM, and GPU.

System POSTed and booted successfully on first power-on.

This confirmed the motherboard as the only component damaged by the surge. PSU, both tested GPUs, the RAM kit, and all 4 SSDs were verified fully functional — avoiding unnecessary replacement spending.


4. Full Rebuild — Micro-ATX Downsize
The surge was used as an opportunity to downsize into a Lian Li A3-mATX case, with GPU length, PSU length, and cooler clearance verified against manufacturer specs before purchase.
4.1 Factory Defect Discovered: Pre-Stripped Screws
6 screws across the PSU bracket, radiator mount, and SSD mount were found pre-stripped from the factory
Confirmed as a factory defect (not user error) by comparing against undamaged front-panel screws from the same case
All 6 removed successfully using a rubber-band-and-driver friction technique
Correct replacement thread spec (6-32 pan-head) identified after an initial mismatch with a countersunk-head screw
4.2 Reassembly & Verification
fTPM/PSP NV reset prompt appeared on first boot with the new board (expected behavior after a CPU/motherboard re-pair)
BitLocker had been disabled proactively on the boot drive beforehand — reset accepted with zero data risk
Final build completed with full cable management, RGB memory, and a 240mm AIO with an integrated LCD pump display


5. Troubleshooting Log
Issue
Root Cause
Resolution
Total room power loss on PC power-on
Electrical surge damaged wall outlet and surge protector simultaneously
Breaker shut off immediately; outlet inspected and replaced before re-powering anything
System failed to POST after surge
Motherboard surge damage (confirmed only after full isolation)
Substituted PSU, GPU, RAM, storage in sequence; replaced motherboard once all else cleared
GPU appeared seated but pulled out easily
Anti-sag support bracket was pushing the card out of full slot contact
Removed bracket, reseated GPU fully into Q-Release Slim latch
PSU bracket screws would not back out
Screws pre-stripped from the factory
Removed via rubber-band-and-driver technique; sourced correct 6-32 replacements
Replacement screw from spare parts bag didn't match
Bag was stocked with countersunk screws, not the pan-head type needed
Visually compared head profile against the original before installing
fTPM/PSP NV reset prompt on first boot
Expected behavior when CPU is paired with a new motherboard
Confirmed BitLocker was already disabled, accepted reset with no data risk



Key Takeaways
A dead surge protector doesn't confirm the full extent of damage — inspect the outlet and wiring independently before re-powering anything
Isolate components by direct substitution, not inference, whenever a known-good spare is available
A barebones boot test (CPU + 1 RAM stick, no GPU, no drives) is the fastest way to narrow a no-POST fault to CPU/motherboard
Anti-sag GPU brackets can mechanically prevent full seating and mimic a hardware failure if misadjusted
Factory-stripped fasteners are a real, recurring defect — compare against known-good screws from the same product to confirm
Disabling BitLocker before a planned board swap removes the single biggest data-loss risk from an fTPM reset



Documentation prepared by Bryan Sykes — August 2026

