# ระบบปรับแต่ง Quest

Fully Guide [here](https://docs.google.com/document/d/1B1qooypdebE2xvJ33cb-BIH5MEEsvi9w4v-vrgcYO1k)

SCUM official tool สำหรับปรับแต่งเควสในเกม SCUM [here](https://drive.google.com/drive/folders/1tITA6KE81awb0G5LYzubK-ZQRAbIKncT)

**โครงสร้างไฟล์มีดังนี้**
สามารถใช้คำสั่ง `#exportQuests` เพื่อสร้างโครงสร้างไฟล์เควสพื้นฐานได้
```js
Quests/
├── Blocked/
│   └── BlockedQuests.json
├── Override/
│   ├── QuestSeriesOne/ // กำลังลอง Test แบบ Sub folder
│   │   └── QuestSeriesOneEP1.json // กำลังลอง Test แบบ Sub folder
│   ├── Questแรก.json
│   └── Questสอง.json
└── QuestList/ // ระบบ Generate ไม่ต้องสนใจ
    ├── CustomQuestList.json
    └── DefaultQuestList.json
```
- `Blocked`: บล็อกเควสเริ่มต้น และเควสอื่นๆ
    ตัวอย่างไฟล์ `BlockedQuests.json`:
    ```json
    {
        "BlockAllDefaultQuests": false, // true เพื่อปิดเควสเริ่มต้นทั้งหมด
        "BlockQuestNames": [
            "DefaultQuest1", // ตัวอย่างชื่อเควสเริ่มต้น
            "เควสนี้จะไม่มีในเกม", // จะส่งผลกับเควสที่มีใน `Override`
        ]
    }
    ```
- `Override`: ใส่ไฟล์เควสที่สร้างเอง (.json ละ 1 เควส)
- `QuestList`: รายการเควสทั้งหมด (แก้ตรงนี้ไม่ส่งผลกับเกม System Generate)

## การสร้างเควส
### โครงสร้างไฟล์เควส
```json
{
  "AssociatedNPC": "Bartender",
  "Tier": 1,
  "Title": "เควสต์แรกของฉัน",
  "Description": "ช่วย Bartender ทำภารกิจ",
  "TimeLimitHours": 24,
  "RewardPool": [ { ... } ],
  "Conditions": [ { ... } ]
}
```
- `AssociatedNPC`: ชื่อ NPC ที่เกี่ยวข้องกับเควส 
  - `Armorer` ร้านขายอาวุธ
  - `Banker` ธนาคาร
  - `Barber` ร้านตัดผม
  - `Bartender` ร้านเหล้า
  - `Doctor` หมอ
  - `Fisherman` | `Harbourmaster` ชาวประมง __ยังงงๆว่าใช้อันไหน__
  - `GeneralGoods` | `General Goods` ร้านขายของทั่วไป
  - `Mechanic` ช่างซ่อมรถ
- `Tier`: ระดับเควส (1-3) ยิ่งสูงยิ่งปลดที่หลัง
- `Title`: ชื่อเควส
- `Description`: คำอธิบายเควส
- `RewardPool`: รายการรางวัลที่ได้รับเมื่อทำเควสสำเร็จ มีได้สูงสุด Reward 5 Slots
  - `CurrencyNormal`,`CurrencyGold`,`Fame`: นับรวม Reward 1 Slot กรอกเป็นเลข
    ```json
        "CurrencyNormal": 1000, 
        "CurrencyGold": 500,
        "Fame": 50
    ```
  - `Skills`: นับ Reward 1 Slot ต่อ Skill กรอกเป็นชื่อ Skill และจำนวนที่ต้องการเพิ่ม เช่น
    ```json
    "Skills": [
        { "Skill": "Survival", "Value": 50 },
        { "Skill": "Cooking", "Value": 50 }
    ] // นับ 2 Slot
    ```
    รายชื่อ Skill (ณ แพตซ์ 1.0) 
    | STR           | CON       | DEX       | INT       
    |-              |-          |-          |-          
    |Boxing         |Running    |Thievery   |Awareness
    |MeleeWeapons   |Endurance  |Demolition |Camouflage
    |Archery        |           |Stealth    |Cooking
    |Rifles         |           |Driving    |Medical
    |Handgun        |           |Motorcycle |Sniping
    |               |           |Aviation   |Survival
    |               |           |           |Engineering
    |               |           |           |Farming
    |               |           |           |Tactics*

    *Tactics เป็น Skill ใหม่ที่เพิ่มเข้ามาในแพตซ์ 1.0
    
    **Tips**: skill มี 4 ระดับ ต้องการ XP ดังนี้
    - `Basic`: 10,000 XP
    - `Medium`: 100,000 XP
    - `Advanced`: 1,000,000 XP
    - `Above Advance`: 10,000,000 XP
  - `TradeDeals`: เปิดขาย / ลดราคาไอเทมที่ NPC ขาย นับ 2 Slot ตาม Deal 1 อัน
    ```json
    "TradeDeals": [
        {
            "Item": "C4",
            "Price": 100,
            "Fame": 10,
            "Amount": 2, 
            "AllowExcluded": true, 
        }// นับ 2 Slot
    ]
    ```
- `Conditions`: เงื่อนไขที่ต้องทำให้สำเร็จเพื่อเคลียร์เควส(สามารถใส่พร้อมกันได้) โดยตั้งค่าเงื่อนไขพื้นฐาน มีดังนี้
  ```json
  {
        "Type": "...",
        "CanBeAutoCompleted": false,
        "TrackingCaption": "Eliminate 3 puppets",
        "SequenceIndex": 0,
        "LocationsShownOnMap": [
            {
                "Location": { "X": 0.0, "Y": 0.0, "Z": 0.0 },
                "SizeFactor": 1.0
            }
        ]
  }
  ```
  - `CanBeAutoCompleted`: ถ้าเป็น `true` จะสามารถเคลียร์เควสได้โดยไม่ต้องกลับไปส่งเควส
  - `TrackingCaption`: ข้อความที่แสดงเมื่อทำเงื่อนไขนี้ เช่น "Eliminate 3 puppets"
  - `SequenceIndex`: ลำดับของเควส (0-4) ถ้าเป็น 0 จะเป็นเงื่อนไขแรกที่ต้องทำ
  - `LocationsShownOnMap`: พิกัดวงกลมที่จะแสดงบนแผนที่เมื่อทำเงื่อนไขนี้ คล้ายกับ `MapSetting`
  - `Type`: ประเภทเงื่อนไขที่ต้องทำให้สำเร็จ มี 3 ประเภทคือ
    - `Elimination`: จัดการสิ่งต่างๆ เช่น NPC, สัตว์, ผี, คน
      - `TargetCharacters`: ชื่อของสิ่งที่ต้องจัดการ
      - `Amount`: จำนวนที่ต้องจัดการ
      - `AllowedWeapons`: อาวุธที่ใช้จัดการได้ (ถ้าไม่ใส่จะใช้ได้ทุกอาวุธ)
    ```json
    {
        "Type": "Elimination",
        // ... ตั้งค่าเงื่อนไขพื้นฐาน ...
        "TargetCharacters": [
            "Prisoner",
            "Puppet",
            "Razor",
            "SentryOld",
            "Sentry",
            "ArmedNPC"
            // ... หรือชื่ออื่นๆ ตาม #SpawnZombie #SpawnAnimal
        ],
        "Amount": 5,
        "AllowedWeapons": [
            "BP_Weapon_M1911_C",
            "BP_Weapon_M9_C"
        ]
    }
    ```
    - `fetch`: เก็บไอเท็มที่กำหนด
      - `DisablePurchaseOfRequiredItems`: ถ้าเป็น `true` จะไม่สามารถซื้อไอเท็มที่ต้องการในสถานที่ต่างๆได้ ยกเว้น Set `QuestRequirementsBlockTradeableItems=0` ใน `ServerSettings`
      - `PlayerKeepsItems`: ถ้าเป็น `true` ผู้เล่นจะเก็บไอเท็มที่เก็บได้ไว้ได้
      - `RequiredItems`: รายการไอเท็มที่ต้องเก็บ
        - `AcceptedItems`: รายชื่อไอเท็มที่ต้องเก็บ
        - `RequiredNum`: จำนวนไอเท็มที่ต้องเก็บ
        - `RandomAdditionalRequiredNum`: จำนวนที่ต้องหาเพิ่มเติม แบบสุ่ม
        - `MinAcceptedItemUses`: จำนวนการใช้งานขั้นต่ำของไอเท็ม
        - `MinAcceptedCookLevel`/`MaxAcceptedCookLevel`: ระดับการปรุงอาหาร เช่น `Raw`, `Undercooked`, `Cooked`, `Overcooked`, `Burned`.
        - `MinAcceptedCookQuality`: คุณภาพการปรุงอาหาร เช่น `Ruined`, `Bad`, `Poor`, `Good`, `Excellent`, `Perfect`.
        - `MinAcceptedItemMass`: มวลขั้นต่ำของไอเท็ม (กรัม)
        - `MinAcceptedItemHealth`: สภาพของไอเท็มขั้นต่ำ %
        - `MinAcceptedItemResourceRatio`: ปริมาตรของเหลวขั้นต่ำ %
        - `MinAcceptedItemResourceAmount`: ปริมาตรของเหลวขั้นต่ำ (ml)
    ```json
    {
        "Type": "Fetch",
        // ... ตั้งค่าเงื่อนไขพื้นฐาน ...
        "DisablePurchaseOfRequiredItems": false,
        "PlayerKeepsItems": false,
        "RequiredItems": [
            {
                "AcceptedItems": [ "Apple" ],
                "RequiredNum": 3,
                "RandomAdditionalRequiredNum": 2,
                "MinAcceptedItemUses": 1,
                "MinAcceptedCookLevel": "Raw",
                "MinAcceptedCookQuality": "Poor",
                "MinAcceptedItemMass": 100.0,
                "MinAcceptedItemHealth": 50.0,
                "MinAcceptedItemResourceRatio": 20.0,
                "MinAcceptedItemResourceAmount": 50.0
            }
        ]
    }
    ```
    - `Interaction`: โต้ตอบกับวัตถุในเกม โดยสามารถใช้ `#GetMeshInfo` เพื่อดูวัตถุที่ใช้โต้ตอบที่มองอยู่ได้ จะได้ Json มาใส่ใน `Locations` ดังนี้
      - `Locations`: รายการวัตถุที่ต้องโต้ตอบ
          - `AnchorMesh`: Mesh ของวัตถุที่ต้องโต้ตอบ (อันนี้จำเป็น)
          - `Instance`: ใช้เมื่อตำแหน่งนั้นมีวัตถุชนิดเดียวกันหลายอันอยู่ใกล้กัน เพื่อระบุ ชิ้นที่ต้องการเฉพาะเจาะจง
          - `FallbackTransform`: ข้อมูลของ `AnchorMesh` ที่จะใช้เมื่อไม่สามารถหาตำแหน่งได้ (เช่น Mesh ไม่อยู่ในมุมมอง) โดยระบุพิกัดและการหมุน
          - `VisibleMesh`: Mesh ที่จะแสดงเมื่อโต้ตอบ (ไม่จำเป็น)
      - `MinNeeded`/`MaxNeeded`: จำนวนขั้นต่ำ/สูงสุดของวัตถุ แบบสุ่มที่ต้องโต้ตอบ
      - `SpawnOnlyNeeded`: 
        - หากตั้งค่าเป็น `true`: → เกมจะสุ่มจำนวนของวัตถุที่ต้องใช้จริง และ จะเกิดขึ้นเฉพาะวัตถุตามจำนวนนั้นเท่านั้น บนแผนที่
        - หากตั้งค่าเป็น `false`: → วัตถุทั้งหมดในรายการจะถูกสร้างขึ้นมา แต่ผู้เล่นไม่จำเป็นต้องโต้ตอบกับทั้งหมด—แค่ครบจำนวนที่กำหนดไว้ก็เพียงพอ
      - `WorldMarkerShowDistance`: ระยะทางที่จะแสดง Marker ใน UI
    ```json
    {
        "Type": "Interaction",
        // ... ตั้งค่าเงื่อนไขพื้นฐาน ...
        "Locations": [
            {
                "AnchorMesh": "/Game/World/SomeMap/BP_Switch.BP_Switch_C",
                "Instance": 4,
                "FallbackTransform": "X=123.456 Y=234.567 Z=10.0 Pitch=0 Yaw=0,Roll=0",
                "VisibleMesh": "/Game/World/SomeMap/BP_SwitchModel.BP_SwitchModel_C" 
            },
            {
                "AnchorMesh": "/Game/World/SomeMap/BP_Door.BP_Door_C"
            }
        ],
        "MinNeeded": 1,
        "MaxNeeded": 2,
        "SpawnOnlyNeeded": true,
        "WorldMarkerShowDistance": 50
    }
    ```
