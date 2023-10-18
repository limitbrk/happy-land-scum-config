## SCUM Loot Modification

Fully Guide [Here](https://docs.google.com/document/d/1TIxj5OUnyrOvnXyEn3aigxLzTUQ-o-695luaaK2PTW0)

สำหรับการตั้งค่า อาจจะใช้ถึง 4 Part ดังนี้ [`Items`](#items) / [`Nodes`](#nodes) / [`Spawners`](#spawners) / [`GeneralZoneModifiers`](#generalzonemodifiersjson)
```js
Loot/
├── Items/
│   └── Override/
│       └── ชื่อไฟล์อะไรก็ได้.json
├── Nodes/
│   └── Override/
│       └── ชื่อไฟล์อะไรก็ได้.json
├── Spawners/
│   └── Presets/
│       └── Override/
│           ├── CustomZone/
│           │   ├── ชื่อไฟล์ที่มีในPreset.json
│           │   └── Zone.json
│           └── ชื่อไฟล์ที่มีในPreset.json
└── GeneralZoneModifiers.json
```
#### ข้อควรรู้ 

`Rarity`
การตั้งค่า ความหายากของไอเทม
```
32 x Abundant
16 x Common
8  x Uncommon
4  x Rare
2  x VeryRare
1  x ExtremelyRare
```

`PostSpawnActions`
การตั้งค่าสภาพไอเทมเมื่อดรอป ใช้ใน [`Nodes`](#nodes) และ [`Spawners`](#spawners)
- `AbandonedBunkerKeycard` - ตั้ง Keycard สำหรับพื้นที่ใกล้ที่สุด
- `SetAmmoAmount_BigStash` - จำนวน Stack 50-100% กระสุนดรอป
- `SetAmmoAmount_SmallStash` - จำนวน Stack 0-35% กระสุนดรอป
- `SetCashAmount_BigStash` - เงินดรอป 200-500
- `SetCashAmount_MediumStash` - เงินดรอป 50-200
- `SetCashAmount_SmallStash` - เงินดรอป 1-100
- `SetClothesDirtiness_DeadPuppets` -  ค่าชุดสกปรก 93-96%
- `SetClothesDirtiness_DirtyClothes` - ค่าชุดสกปรก 60-85%
- `SetClothesDirtiness_ResidentialClothes` - ค่าสกปรก 0-20%
- `SetUsage_Max` - ดรอปชาร์จเต็ม

### `Items/`

เป็นการกำหนด Spawn Item

สามารถตั้งชื่อไฟล์อะไรก็ได้เพื่อเพิ่มหรือแก้
```json
{
	"Parameters": [
		{
			"Id": "Weapon_M82A1",
			"IsDisabledForSpawning": false,			// ปิดการ Spawn
			"AllowedLocations": [                           // เลือกพื้นที่ที่ดรอป
				"Coastal", 				// - ชายหาด
				"Continental", 				// - พื้นดิน
				"Mountain" 				// - ภูเขา
			],
			"CooldownPerSquadMemberMin": 0, 		// 1Squad จะไม่เจอไอเทมนี้อีกเลย (Min~Max)*members ชั่วโมง
			"CooldownPerSquadMemberMax": 0,
			"Variations": [ 				// สุ่ม Spawn ของตามนี้ด้วย
				"Weapon_M82A1_Black",
				"Weapon_M82A1_Desert",
				"Weapon_M82A1_Snow"
			],
			"ShouldOverrideInitialAndRandomUsage": false, 	// เปิดการตั้งค่าด้านล่างทับ Presets
			"InitialUsageOverride": 0, 			// หัก ขาร์จไอเทม ค่าคงตัว
			"RandomUsageOverrideUsage": 0 			// หัก ขาร์จไอเทม ค่าสุ่มจาก 0
		}
    ]
}
```

### `Nodes/`

เป็น Set [Items](#items) ที่ไว้ใช้ Spawn เพื่อใช้ผ่าน [Spawner Preset](#spawners)

ดูผลลัพธ์ได้ผ่านคำสั่ง โดยจะลงใน `Loot/Nodes/Current/`
```
#ExportCurrentLootTree
```

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
							"Rarity": "Abundant", 	// ระดับความหายาก
							"Variations": [ 	// สุ่ม Spawn ของตามนี้ด้วย
				 				"PETBottle02",
 								"PETBottle03",
 								"PETBottle04"
 							],
							"PostSpawnActions": []  // ตั้งค่าสภาพดรอป
						}
					]
				}
			]
		}
	]
}
```

### `Spawners/`
เป็น ID ของ Object บนโลก โดย 1 Object สามารถมีหลาย [Spawner Preset](#spawners)

Object ไหนเวลาค้นหาใช้ [Spawner Preset](#spawners) อะไร สามารถดูได้ที่ (แล้วกดค้นหา)
```
#SetShouldPrintExamineSpawnerPresets true 
```
![Spawner Preset Show](https://imgur.com/hpuuy0I.png)
โดยมีวิธีการใช้งาน 2 แบบ
- _แบบ Global_ สามารถวางที่ Folder `Loot/Spawners/Presets/Override/`
- _แบบ Zone_ ทำตามนี้ สร้างไฟล์อัตโนมัติ `Loot/Spawners/Presets/Override/ชื่อโซน/`
  ```
  #ExportItemSpawnerPresetsInZone A1
  #ExportItemSpawnerPresetsInZone X1 Y1 X2 Y2 ตั้งชื่อโซน
  ```
  _X1,Y1 คือพิกัดมุมซ้ายบน X2,Y2 คือพิกัดมุมขวาล่าง_

ในไฟล์ `ชื่อไฟล์ที่มีในPreset.json` จะเป็น Preset ที่มีอยู่แล้ว โดยสามารถใช้ [Items](#items) / [Nodes](#nodes)
ส่วนใช้ [Spawners](#spawners) จะอธิบายใน [Subpreset](#subpreset)
```json
{   
 	"Nodes": [ 				// ตั้งโอกาส Node ที่มี หรือเราสร้าง
		{
			"Rarity": "Uncommon",
			"Ids": [
				"ItemLootTreeNodes.Trash",
			]
		}
	],
	"Items": [ 				// ตั้งโอกาส Item ดรอป
		{
			"Rarity": "Abundant",
			"Id": "Stone_Small"             
		}
	],
	"FixedItems": [  			// ตั้ง Item ดรอป 100% ตามจำนวน (ซ้ำได้)
		"Stone_Small"
	],
	"Probability": 20, 			// โอกาสดรอป%
	"QuantityMin": 0, 			// จำนวนที่ดรอปสูง-ต่ำ (ไม่รวม Fixed)
	"QuantityMax": 0,
	"AllowDuplicates": true, 		// ให้ไอเทมเกิดซ้ำได้
	"ShouldFilterItemsByZone": false, 	// ใช้ค่าจาก Items>AllowedLocations
	"InitialDamage": 0, 			// หัก %ไอเทม ค่าคงตัว
	"RandomDamage": 0, 			// หัก %ไอเทม ค่าสุ่มจาก 0
	"InitialUsage": 0, 			// หัก ขาร์จไอเทม ค่าคงตัว
	"RandomUsage": 0 			// หัก ขาร์จไอเทม ค่าสุ่มจาก 0
	"PostSpawnActions": []  		// ตั้งค่าสภาพดรอป
}
```
ในไฟล์ `Zone.json` จะกำหนดพื้นที่ของ [Spawner Preset](#spawners) (เฉพาะแบบกำหนด Zone)
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
ก็คือพิกัดมุมซ้ายบน มุมขวาล่าง เหมือนตอนใช้ Command

#### Subpreset
รวม [Spawners](#spawners) ย้อยๆมาใส่ไว้ใน [Spawners](#spawners) เดียว
```json
{
	"Subpresets": [
		{
			"Rarity": "Uncommon",
			"Id": "Special_Packages-Vault-Examine_AWP_Vault_Pack"
		},
		{
			"Rarity": "Uncommon",
			"Id": "Special_Packages-Vault-Examine_AWP_Ammo_Vault_Pack"
		}
	]
}
```

### `GeneralZoneModifiers.json`

เป็นการตั้งพื้นที่เพื่อเพิ่ม Rate Drop (ต้องสร้างไฟล์เอง)
```json
{
	"Modifiers": [
		{
			"Zones": [ 					// Zone พิกัดซ้ายบน-ขวาล่าง
				{
					"Name": "FishFactory", 		// ตั้งชื่ออะไรก็ได้
					"TopLeft": "X=-327211.8142 Y=-346843.5702",
					"BottomRight": "X=-363868.8911 Y=-383500.647"
				}
			],
			"SpawnerProbabilityMultiplier": 100, 		// Rate Drop พื้น
			"ExamineSpawnerProbabilityMultiplier": 100, 	// Rate Drop ค้น
			"ExamineSpawnerQuantityMultiplier": 5 		// Rate จำนวน ค้น
		},
		{
			"Zones": [ 					// Zone Sector
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

> จำเป็นต้องใส่ ทุก Parameter ไหม
> ``` 
> บางอันไม่จำเป็น จะไปตั้งตามค่า Default
> ```

> ทำไมไม่แก้ `Default/` แทน
> ``` 
> แก้ไปก็ไม่มีอะไรเกิดขึ้น ลองแล้ว และมันจะทำให้เรา Revert ที่เราทำได้ง่ายด้วย
> ```

> [Spawner Preset](#spawners) ต้องใช้ทุกไฟล์ ตาม ExportZone ไหม
> ``` 
> ไม่ต้อง ลบที่ไม่ต้องการ Override ได้ เพื่อประหยัดที่ Disk
> ```

> [Spawner Preset](#spawners) Global ต้องทำยัง
> ``` 
> วางไว้ที่ Loot/Spawners/Presets/Override ได้เลย
> ```

> อัพขึ้น Server ยังไง
> ``` 
> FTP ไม่ก็ Host บางเจ้ามี FileManager ก็อัพไปที่
> Multi - <Server>\SCUM\Saved\Config\WindowsServer\Loot
> Single- %LocalAppData%\SCUM\Saved\Config\WindowsNoEditor\Loot
> ```

> Apply ยังไง ต้อง Re-Server ไหม
> ``` 
> ไม่ต้อง ใช้คำสั่งนี้แทนได้ 
> #ReloadLootCustomizationsAndResetSpawners
> ```
