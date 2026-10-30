# SBT-DF205-Case-2-iOS-Forensics-Investigation-of-an-iPhone-SE
# iOS Forensics Investigation: iPhone SE (iOS 13.4.1)

**International Cybersecurity and Digital Forensics Academy (ICDFA)**
School of Basic Vocational Training (SVT)

![Course](https://img.shields.io/badge/Course-SBT--DF205-red)
![Case Study](https://img.shields.io/badge/Case%20Study-02%20iOS%20Forensics-blue)
![Tools](https://img.shields.io/badge/Tools-SQLite%20%7C%20plistutil%20%7C%20Kali%20Linux-informational)
![Status](https://img.shields.io/badge/Status-Complete-darkgreen)

---

### Author Information & Copyright

| Field | Details |
| :--- | :--- |
| **Student Name** | Ibrahim Diseh Garba |
| **Student ID** | 2025/FWSD/11521 |
| **Programme** | Fellowship in Web Application Security & Digital Forensics |
| **Course** | SBT-DF205 - Mobile and IoT Forensics Case Study |
| **Instructor** | Aminu Idris, AMCPN |
| **Date** | 29th October, 2026 |
| **Case Reference** | SBT-DF205-C2 |

**Copyright Notice:** © 2026 Ibrahim Diseh Garba. All Rights Reserved. 
This work is submitted as part of the Fellowship in Web Application Security & Digital Forensics at ICDFA. Please refer to the [Copyright & Usage](#-copyright--usage) section below for usage permissions.

---

### Executive Summary

This repository contains the forensic artefacts, SQL scripts, and final report for an examination of an **iPhone SE (1st Generation) running iOS 13.4.1**. The investigation was conducted to establish how the device was used and to reconstruct user activity.

> **Primary Findings:** The device belongs to the user **"Thisisdifi"** and is linked to the iCloud account `thisisdifi@gmail.com`. Artefacts relating to messaging, Safari browsing, health activity, and location were successfully recovered. Safari history shows the user searched for sports news in late March 2020. Health records contain step counts and walking distances, and location records place the device in the Raleigh, North Carolina area.
> 
> **Confidence Level:** High for both device identification and artefact recovery. Every timestamp was converted from Apple Cocoa Core Data format to UTC so that events could be placed in the correct chronological order.

---

### Key Findings & Artefacts

### Device Identification & Accounts
*   **Device Model:** iPhone8,4 (iPhone SE)
*   **iOS Version:** 13.4.1 (Build: 17E262)
*   **Serial Number:** `DX3T126VH2XV`
*   **Account:** `thisisdifi@gmail.com`
*   **Location Services:** Enabled
*   **iCloud Backup:** Enabled

### Communications & Media
*   **SMS/iMessage (`sms.db`):** Recovered messages, including Siri dictation test messages (e.g., *"This is your second test message for Siri dictation"*) and an SMS notification for a new Facebook friend.
*   **Call History (`CallHistory.storedata`):** Recovered recent calls associated with the number `+14082567000`.
*   **Media (`Photos.sqlitedb`):** Identified camera roll and saved images, including files like `IMG_0001.JPG` and `IMG_0727.JPG`.
*   **Calendar (`Calendar.sqlitedb`):** Empty (no stored calendar events).

### Web Browsing
*   **Safari History (`History.db`):** Recovered Google searches from March 28, 2020, indicating an interest in sports news:
    *   *"When does mlb start 2020 - Google Search"*
    *   *"Is the NHL going to resume? - Google Search"*

### Health & Location Data
*   **Health (`healthdb_secure.sqlite`):** Recovered step counts and walking distances. For example, on March 24, 2020, the device logged **5,951 steps** (4,704 metres) and burned 525 kcal.
*   **Location (`Local.sqlite`):** The `ZRTLEARNEDLOCATIONOFINTERESTVISITMO` table places the user in the Raleigh, North Carolina area (Latitude: `35.659`, Longitude: `-78.872`) on April 11, 2020.

---

### Evidence Handling & Integrity

### Evidence Source
*   **Dataset:** Digital Corpora (Joshua Hickman iOS 13.4.1 dataset)
*   **Source Archives:** `ios_13_4_1.zip` and `13-4-1.tar`
*   **Working Copy Location:** `~/SBT-DF205-C2/iOS 13.4.1 Extraction/Extraction/`

### Integrity Verification (SHA-256)
*   **ZIP Hash:** `761854a669c38da6ac0a908afe77763d54ccb83044ff123350890d408c154551`
*   **TAR Hash:** `991727d92145a08623e998c008cc2a05f086be722ee2945815d0eb46a78f04fb`

### Tools Used
| Tool | Version | Purpose |
| :--- | :--- | :--- |
| **Kali Linux** | Rolling | Analysis environment |
| **SQLite3** | 3.40.0 | Command-line database queries |
| **DB Browser for SQLite** | 3.13.1 | GUI database navigation and verification |
| **plistutil** | libplist-utils | Reading binary/XML plist files |

---

### Key SQL Queries Used

The repository includes the `Queries.sql` file, but here are the core commands used to extract the evidence:

**Call History (Apple Cocoa Core Data Timestamp conversion):**

---

### Challenges & Limitations
Attribution Gap: The device data proves the phone was in use, but it cannot establish who was physically holding it at any given moment (e.g., the owner, a family member, or a colleague).

Empty Databases: Several expected artefacts were missing. The Calendar database held no events, and some app data may have been cleared by the user or not captured during the extraction process.

Timestamp Complexity: iOS stores timestamps in Apple Cocoa Core Data format (seconds since January 1, 2001). While these were successfully converted to UTC, any manual miscalculation could skew the timeline.

Logical vs. Physical Extraction: This analysis relies on a logical/file-system extraction. Deleted records (e.g., deleted SMS or Safari history) may only be recoverable via a full physical extraction or by examining unallocated space.

---

### Recommendations
For the Investigation
Seek Corroborating Evidence: To bridge the attribution gap, obtain biometric records (FaceID/TouchID logs), CCTV footage, or HR records that place a specific individual in the Raleigh, NC area on April 11, 2020.

Check iCloud Backups: Since iCloud Backup was enabled, law enforcement should issue a legal request to Apple for the iCloud backup associated with thisisdifi@gmail.com to recover data not present on the local device (e.g., deleted Safari history or calendar entries).

Perform Physical Extraction: If the device is available, consider using a tool like Cellebrite UFED or GrayKey for a full physical extraction to recover deleted SQLite records.

For Device Security (Organisational)
Enforce MDM Policies: If this were a corporate device, Mobile Device Management (MDM) should be deployed to log app usage, enforce passcodes, and remotely wipe data if lost.

Restrict iCloud Backups: For corporate devices, restrict iCloud backups to prevent sensitive company data from syncing to personal Apple accounts.

---

### Conclusion
The forensic examination successfully reconstructed user activity from the iPhone SE extraction. The evidence indicates that the device owner (linked to thisisdifi@gmail.com) was present in the North Carolina area, looked up sports news in late March 2020, and logged physical activity data.

The SMS, Safari, Health, and Location databases agree with one another and together support a timeline of ordinary device use. However, a critical limitation remains: the device data shows that the phone was in use, but it cannot establish who was physically holding it. Establishing human identity would require further corroborating evidence, such as biometric records or video footage.

```sql
SELECT ZADDRESS, ZDATE, ZDURATION, ZORIGINATED 
FROM ZCALLRECORD 
ORDER BY ZDATE DESC LIMIT 5;

Copyright & Usage
© 2026 Ibrahim Diseh Garba. All Rights Reserved.

This repository contains academic coursework and a forensic report submitted as part of the Fellowship in Web Application Security & Digital Forensics at the International Cybersecurity and Digital Forensics Academy (ICDFA).
