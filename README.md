# ⚡ Electrical Surge Incident Response & PC Rebuild

![Diagnosis](https://img.shields.io/badge/Method-Systematic_Component_Isolation-2ea44f?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Resolved-2ea44f?style=for-the-badge)
![Outcome](https://img.shields.io/badge/Result-1_of_6_Components_Replaced-0078D4?style=for-the-badge)

**Analyst:** Bryan Sykes | **Date:** July 2026

Full write-up: [`docs/electrical-surge-incident-response-and-rebuild.pdf`](docs/electrical-surge-incident-response-and-rebuild.pdf)

---

## The Short Version

A thunderstorm knocked out power to my desktop mid-boot. Instead of guessing at what broke and replacing parts until something worked, I treated it like a hardware incident: isolate the circuit, isolate each component with direct substitution, and only replace what the evidence pointed to. Six major components were tested. Five came back clean. One — the motherboard — was the actual casualty, confirmed, and replaced. I used the rebuild as a chance to downsize the whole system into a smaller case at the same time.

This project is really about the process, not the parts: assume nothing, test one variable at a time, and don't throw money at a problem you haven't isolated yet. That's the same discipline that applies to diagnosing a "network issue" that's actually a bad cable, or a "software bug" that's actually a permissions problem.

| | |
|---|---|
| **Trigger event** | Thunderstorm-related electrical surge; wall outlet and surge protector both failed |
| **Systems affected** | Desktop PC (AM5 / Ryzen 5 9600X / RTX 4080 Super), room electrical circuit |
| **Root cause** | ASUS ROG Strix B850-A Gaming WiFi motherboard — the sole failed component |
| **Method** | Direct visual inspection plus component substitution testing, no assumptions |
| **Outcome** | Root cause isolated with zero unnecessary part replacement; full rebuild completed into a smaller case |

---

## 1. Electrical Hazard Assessment

A power flash caused total room power loss while powering on the PC. Rather than assuming the surge protector alone absorbed the event, the outlet itself was inspected directly.

- The breaker for the affected room was shut off before any further inspection.
- The wall outlet showed visible burn and scorch damage on the hot-side contact, confirming the surge protector wasn't the only casualty.
- The damaged surge protector (scorched prong) was retired.
- The outlet was replaced before anything was reconnected to that circuit.

| | |
|---|---|
| ![](photos/01-wall-outlet-burn-damage.jpg) | ![](photos/05-surge-protector-burn-damage.jpg) |
|:---:|:---:|
| Wall outlet: visible burn damage on the hot-side contact | Surge protector: scorched prong |

---

## 2. Component Isolation Testing

Every major component was cleared through direct substitution, one variable at a time, rather than guesswork.

### 2.1 Power Supply

The original DeepCool 1000W PSU delivered standby power, but the system still failed to POST. A second, brand-new PSU was swapped in as a control; the identical failure persisted, which cleared the PSU. The control unit was returned for a full refund.

### 2.2 Graphics Card

The primary GPU (PNY RTX 4080 Super) was reseated and its 12VHPWR connector inspected; no pin damage. A second known-good GPU was substituted into the same slot and produced the identical failure, clearing both GPUs.

![](photos/11-known-good-gpu-substitution-test.jpg)

*Substitution test: a second, known-good GPU in the same slot still failed to POST — the GPU was not the problem.*

### 2.3 Memory

The T-Force Delta DDR5 RGB kit was visually inspected; contacts clean, no damage. A barebones boot test (one stick, no GPU, no drives) still failed, which cleared the RAM.

| | |
|---|---|
| ![](photos/08-ram-modules-removed.jpg) | ![](photos/09-ram-contact-inspection-a.jpg) |
|:---:|:---:|
| RAM removed for inspection | Contact inspection: clean, no damage |

### 2.4 Storage

All 4 SSDs were pulled and verified individually through an external enclosure on a separate laptop. All 4 came back healthy and readable: zero data loss, storage cleared.

### 2.5 CPU and Socket

CPU contact pads were inspected under multiple lighting angles; no scorching or corrosion. A full barebones test (CPU plus one RAM stick, no GPU, no drives) still failed to POST. With no spare AM5 board or CPU on hand to cross-test against, a replacement motherboard became the only remaining way to isolate CPU from motherboard.

| | |
|---|---|
| ![](photos/12-cpu-contact-pad-inspection-a.jpg) | ![](photos/13-cpu-contact-pad-inspection-b.jpg) |
|:---:|:---:|
| CPU contact pads, angle A: no scorching or corrosion | CPU contact pads, angle B |

![](photos/02-diagnostic-leds-stuck-vga-boot.jpg)

*The motherboard's onboard diagnostic LEDs stuck on VGA and BOOT through every substitution — the first real clue pointing at the board itself.*

---

## 3. Root Cause Confirmation

A new ASUS ROG Strix B850-A Gaming WiFi motherboard was installed with the original CPU, RAM, and GPU. The system POSTed and booted successfully on the first power-on.

That confirmed the motherboard as the only component the surge damaged. The PSU, both tested GPUs, the RAM kit, and all 4 SSDs were verified fully functional, avoiding unnecessary replacement spending.

![](photos/14-motherboard-confirmed-fried.jpg)

*The original motherboard, confirmed dead and no longer usable.*

---

## 4. Full Rebuild — Case Downsize

The surge was used as an opportunity to downsize into a Lian Li A3-mATX case. GPU length, PSU length, and cooler clearance were checked against manufacturer specs before buying anything.

### 4.1 Factory Defect: Pre-Stripped Screws

Six screws across the PSU bracket, radiator mount, and SSD mount turned out to be pre-stripped from the factory. Comparing them against the case's undamaged front-panel screws confirmed it was a factory defect, not user error. All six were removed with a rubber-band-and-driver friction technique, and the correct replacement thread spec (6-32 pan-head) was identified after an initial mismatch with a countersunk-head screw.

| | |
|---|---|
| ![](photos/15-stripped-psu-bracket-screw-a.jpg) | ![](photos/16-stripped-psu-bracket-screw-b.jpg) |
|:---:|:---:|
| Stripped PSU bracket screw, angle A | Stripped PSU bracket screw, angle B |

![](photos/17-front-panel-screws-undamaged-comparison.jpg)

*Undamaged front-panel screws from the same case, used as the comparison that confirmed a factory defect rather than user error.*

![](photos/18-all-stripped-screws-removed.jpg)

*All six stripped screws removed and replaced.*

### 4.2 Reassembly and Verification

An fTPM/PSP NV reset prompt appeared on first boot with the new board, which is expected after a CPU and motherboard are re-paired. BitLocker had already been disabled on the boot drive beforehand, so the reset was accepted with zero data risk. The final build was completed with full cable management, RGB memory, and a 240mm AIO with an integrated LCD pump display.

| | |
|---|---|
| ![](photos/03-final-build-lcd-cooler.jpg) | ![](photos/04-final-build-cable-management.jpg) |
|:---:|:---:|
| Final build: 240mm AIO with LCD pump display | Final build: cable management |

---

## Troubleshooting Log

| Issue | Root cause | Resolution |
|---|---|---|
| Total room power loss on PC power-on | Electrical surge damaged the wall outlet and surge protector simultaneously | Shut off the breaker immediately; inspected and replaced the outlet before re-powering anything |
| System failed to POST after the surge | Motherboard surge damage, confirmed only after full isolation | Substituted PSU, GPU, RAM, and storage in sequence; replaced the motherboard once everything else cleared |
| GPU appeared seated but pulled out easily | The anti-sag support bracket was pushing the card out of full slot contact | Removed the bracket, reseated the GPU fully into the latch |
| PSU bracket screws would not back out | Screws pre-stripped from the factory | Removed with a rubber-band-and-driver technique; sourced the correct 6-32 replacements |
| Replacement screw from the spare parts bag didn't fit | The bag was stocked with countersunk screws, not the pan-head type needed | Compared the head profile against the original before installing |
| fTPM/PSP NV reset prompt on first boot | Expected behavior when a CPU is paired with a new motherboard | Confirmed BitLocker was already disabled, accepted the reset with no data risk |

![](photos/06-motherboard-idle-power-from-psu.jpg)

*Checked for idle standby power from the PSU as part of ruling components in or out before swapping anything.*

![](photos/07-pcie-slot-inspection.jpg)

*PCIe slot inspection on the original motherboard.*

![](photos/10-ram-contact-inspection-b.jpg)

*Second angle on the RAM contact inspection.*

---

## Key Takeaways

- A dead surge protector doesn't tell you the full extent of the damage. Inspect the outlet and wiring independently before re-powering anything.
- Isolate components by direct substitution, not inference, whenever a known-good spare is available.
- A barebones boot test (CPU plus one RAM stick, no GPU, no drives) is the fastest way to narrow a no-POST fault down to CPU or motherboard.
- Anti-sag GPU brackets can mechanically prevent a card from fully seating and mimic a hardware failure if they're misadjusted.
- Factory-stripped fasteners are a real, recurring defect. Compare against known-good screws from the same product to confirm it before assuming you stripped them yourself.
- Disabling BitLocker before a planned board swap removes the single biggest data-loss risk from an fTPM reset.

---

## Skills Demonstrated

Root-cause hardware diagnosis, systematic component isolation (control-variable testing), electrical safety assessment, PC assembly and disassembly, cable management, data-loss prevention (BitLocker/TPM awareness before a board swap), and clear incident documentation.

---

## Repository Layout

```
.
├── README.md
├── docs/
│   └── electrical-surge-incident-response-and-rebuild.pdf
└── photos/              # 18 numbered photos, 01 to 18
```

---

*Bryan Sykes | Home Lab Portfolio | August 2026*
