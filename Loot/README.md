## SCUM Loot Modification

Fully Guide [Here](https://docs.google.com/document/d/1TIxj5OUnyrOvnXyEn3aigxLzTUQ-o-695luaaK2PTW0)

สำหรับการตั้งค่า อาจจะใช้ถึง 4 Part ดังนี้ `Items / Nodes / Spawners / GeneralZoneModifiers`
```js
Loot/
├── Items/
│   └── Override/
│       └── ชื้อไฟล์อะไรก็ได้.json
├── Nodes/
│   └── Override/
│       └── ชื้อไฟล์อะไรก็ได้.json
├── Spawners/
│   └── Presets/
│       └── Override/
│           ├── CustomZone/
│           │   ├── ชื่อไฟล์ที่มีในPreset.json
│           │   └── Zone.json
│           └── ชื่อไฟล์ที่มีในPreset.json
└── GeneralZoneModifiers.json
```
### Rarity*
ความหายากของไอเทม
```
32 x Abundant
16 x Common
8  x Uncommon
4  x Rare
2  x VeryRare
1  x ExtremelyRare
```

### Items

เป็นการกำหนด Spawn Item

สามารถตั้งชื่อไฟล์อะไรก็ได้เพื่อเพิ่มหรือแก้
```json
{
	"Parameters": [
		{
			"Id": "Weapon_M82A1",
			"IsDisabledForSpawning": false,                 // ปิดการ Spawn
			"AllowedLocations": [                           // เลือกพื้นที่ที่ดรอป
				"Coastal",                                  // - ชายหาด
				"Continental",                              // - พื้นดิน
				"Mountain"                                  // - ภูเขา
			],
			"CooldownPerSquadMemberMin": 0,                 // 1Squad จะไม่เจอไอเทมนี้อีกเลย (Min~Max)*members ชั่วโมง
			"CooldownPerSquadMemberMax": 0,
			"Variations": [                                 // สุ่ม Spawn ของตามนี้ด้วย
				"Weapon_M82A1_Black",
				"Weapon_M82A1_Desert",
				"Weapon_M82A1_Snow"
			],
			"ShouldOverrideInitialAndRandomUsage": false,   // เปิดการตั้งค่าด้านล่างทับ Presets
			"InitialUsageOverride": 0,                      // หัก ขาร์จไอเทม ค่าคงตัว
			"RandomUsageOverrideUsage": 0                   // หัก ขาร์จไอเทม ค่าสุ่มจาก 0
		}
    ]
}
```

### Nodes

เป็น Set Item ที่ไว้ใช้ Spawn เพื่อใช้ผ่าน Spawners

สามารถตั้งชื่อไฟล์อะไรก็ได้เพื่อเพิ่มหรือแก้
```json
{
	"Name": "ItemLootTreeNodes",
	"Children": [                                    
		{
			"Name": "Trash",
			"ChildrenMergeMode": "Replace",         // เลือกวิธีตั้งค่า Replace คือวางทับ UpdateOrAddคือรวม
			"Children": [                           // แบ่ง Set ตามรายละเอียด
				{
					"Name": "Drinks",
					"Rarity": "Abundant",
					"Children": [
						{
							"Name": "PETBottle01",
							"Rarity": "Abundant",   // ระดับความหายาก
							"Variations": [         // สุ่ม Spawn ของตามนี้ด้วย
                                "PETBottle02",
                                "PETBottle03",
                                "PETBottle04",
                            ],
						}
					]
				}
			]
		}
	]
}
```

### Spawners
เป็น ID ของ Object บนโลก โดย 1 Object สามารถมีหลาย ID

Object ไหน ID อะไร สามารถดูได้ที่ (แล้วกดค้น)
```
#SetShouldPrintExamineSpawnerPresets true 
```
ถ้าตั้ง Global สามารถวางที่ Folder `Loot/Spawners/Presets/Override/` ได้เลย

แต่ถ้าตั้ง ตาม Zone ทำตามนี้ได้ (เพิ่มลบไฟล์ที่ใช้ที่หลังได้)
```
#ExportItemSpawnerPresetsInZone A1
#ExportItemSpawnerPresetsInZone X1 Y1 X2 Y2 ตั้งชื่อโซน
```
_X1,Y1 คือพิกัดมุมซ้ายบน X2,Y2 คือพิกัดมุมขวาล่าง_

ในไฟล์ `ชื่อไฟล์ที่มีในPreset.json` จะเป็น Preset ที่มีอยู่แล้ว
```json
{   
    "Nodes": [                              // ตั้งโอกาส Node ที่มี หรือเราสร้าง
		{
			"Rarity": "Uncommon",
			"Ids": [
				"ItemLootTreeNodes.Trash",
			]
		}
	],
	"Items": [                              // ตั้งโอกาส Item ดรอป
		{
			"Rarity": "Abundant",
			"Id": "Stone_Small"             
		}
	],
	"FixedItems": [                         // ตั้ง Item ดรอป 100% ตามจำนวน (ซ้ำได้)
		"Stone_Small"
	],
	"QuantityMin": 0,                       // จำนวนที่ดรอปสูง-ต่ำ (ไม่รวม Fixed)
	"QuantityMax": 0,
	"AllowDuplicates": true,                // ให้ไอเทมเกิดซ้ำได้
	"ShouldFilterItemsByZone": false,       // ใช้ค่าจาก Items>AllowedLocations
	"InitialDamage": 0,                     // หัก %ไอเทม ค่าคงตัว
	"RandomDamage": 0,                      // หัก %ไอเทม ค่าสุ่มจาก 0
	"InitialUsage": 0,                      // หัก ขาร์จไอเทม ค่าคงตัว
	"RandomUsage": 0                        // หัก ขาร์จไอเทม ค่าสุ่มจาก 0
}
```
ในไฟล์ `Zone.json` จะกำหนดพื้นที่ของ Preset
```json
{
	"Zones": [
		{
			"TopLeft": "X=597980 Y=-754329",
			"BottomRight": "X=542036 Y=-798699"
		}
	]
}
```
ก็คือพิกัดมุมซ้ายบน มุมขวาล่าง เหมือนตอนใช้ Command นั่นแหละ

### GeneralZoneModifiers.json

เป็นการตั้งพื้นที่เพื่อเพิ่ม Rate Drop (ต้องสร้างไฟล์เอง)
```json
{
	"Modifiers": [
		{
			"Zones": [                                      // Zone พิกัดซ้ายบน-ขวาล่าง
				{
					"Name": "FishFactory",                  // ตั้งชื่ออะไรก็ได้
					"TopLeft": "X=-327211.8142 Y=-346843.5702",
					"BottomRight": "X=-363868.8911 Y=-383500.647"
				}
			],
			"SpawnerProbabilityMultiplier": 100,            // Rate Drop พื้น
			"ExamineSpawnerProbabilityMultiplier": 100,     // Rate Drop ค้น
			"ExamineSpawnerQuantityMultiplier": 5           // Rate จำนวน ค้น
		},
		{
			"Zones": [                                      // Zone Sector
				{
					"Sector": "A1"
				}
			],
			"ExamineSpawnerQuantityMultiplier": 5
		}
	]
}
```

### FAQ
> ของที่ไม่ดรอป ปล่อยดรอปได้ไหม
> ``` 
> ลองชุดกันผีแล้ว ไม่ได้ (ของไม่ดรอปบนโลกคือไม่ได้)
> ```


> อัพขึ้น Server ยังไง
> ``` 
> FTP ไม่ก็ Host บางเจ้ามี FileManager
> ```