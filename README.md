# serv-cda-allstack
serv-cda-allstack to manage all tech stacks of JD technology

## Current issues
1. The repositories were not well designed for collaborative work, due to architecture designs, embeded libraries.
2. There are no independent databases, all configs were embeded into the code.
3. All codes need to be rebuilt each time there were some minor updates or patch.
4. No single management platform to configure.

## TASKS

### 1. CDA-directory
- db: ocare_cda, collection: directory_level_1, document: list of items


 CRUD item in: 
- document: item, selected NameEn
```
 [
  {
    "Id": 1,
    "Name": "ตรวจร่างกาย",
    "NameEn": "Physical Examination",
    "Acronym": "PE",
    "DisplayOrder": 1
  },
  {
    "Id": 3,
    "Name": "ระบบเลือด",
    "NameEn": "Hematology",
    "Acronym": "HEME",
    "DisplayOrder": 2
  }
 ]
```
- db: ocare_cda, collection: directory_level_2, document: list of items

Tasks

 CRUD item in: 
- document: item, selected NameEn
```
 [
  {
    "Id": 1,
    "Id_lv1": 2,
    "Id_lv2": 1,
    "Name": "การได้ยิน",
    "NameEn": "Audiogram",
    "Acronym": "(Audiogram)",
    "Remark": "Audiog",
    "Instruction": "",
    "Status": "0",
    "ValueMax": "1",
    "ValueMin": "1",
    "Unit": "",
    "Price": "",
    "DisplayOrder": 27,
    "CallName": "Audiogram",
    "OcareCode": "",
    "Order": 412
  },
  {
    "Id": 2,
    "Id_lv1": 2,
    "Id_lv2": 1,
    "Name": "ประวัติการได้ยิน",
    "NameEn": "Hearing History",
    "Acronym": "(Hearing History)",
    "Remark": "Hearing",
    "Instruction": "",
    "Status": "0",
    "ValueMax": "",
    "ValueMin": "",
    "Unit": "",
    "Price": "",
    "DisplayOrder": 28,
    "CallName": "HearingHi",
    "OcareCode": "",
    "Order": 413
  }
]
```
- db: ocare_cda, collection: directory_level_3, document: list of items

Tasks

 CRUD item in: 
- document: item, selected NameEn
```
[
	{
    "Id": 640,
    "Id_lv1": 2,
    "Id_lv2": 9,
    "Name": "กรดเมทิลฮิพพูริกในเลือด",
    "NameEn": "Methyl Hippuric Acid in Blood",
    "Acronym": "(Methyl Hippuric acid in Blood)",
    "Remark": "Methyl Hippuric Acid in Blood",
    "Instruction": "",
    "Status": "1",
    "ValueMax": "",
    "ValueMin": "",
    "Unit": "",
    "Price": "",
    "DisplayOrder": 41,
    "CallName": "MethylHippuricAcidBlood",
    "OcareCode": "",
    "Order": 535
  },
  {
  "Id": 641,
  "Id_lv1": 2,
  "Id_lv2": 9,
  "Name": "แมงกานีสในปัสสาวะ",
  "NameEn": "Manganese (Mn) in Urine",
  "Acronym": "(Manganese (Mn) in Urine)",
  "Remark": "Manganese (Mn) in Urine",
  "Instruction": "",
  "Status": "1",
  "ValueMax": "3",
  "ValueMin": "0",
  "Unit": "ug/g.Creatinine",
  "Price": "",
  "DisplayOrder": 958,
  "CallName": "ManganeseUrine",
  "OcareCode": "",
  "Order": 535
  }
]
```
- db: ocare_cda, collection: directory_level_3_upload_mapping, document: list of items

Tasks

 CRUD item in: 
- collection
- document: item, selected organization
```
[
{
  "organization" : "nhealth",
  "item":
{
	"HN": [
		""
	],
	"FirstName": [
		"EPVIS_GivenName"
	],
	"LastName": [
		"EPVIS_Surname"
	],
	"IDCard": [
		"EPVIS_PatientAddress1"
	],
	"Uric acid": [
		"C0320",
		"C120",
		"C1729"
	],
	"Urine Amphetamine": [
		"V0726"
	]
}
}
]
```

### 2. CDA-model-expert
- link json library (L2, library) to NoSQLDB

- db: ocare_cda, collection: model_expert_L2_ref, document: list of items with tag item_lv2_NameEn and normal_list/ borderline_list/ abnormal_list/ notexamined_list

Tasks

 CRUD item in: 
- collection
- document: item, selected item_lv2_nameen

```
[
    {
        "item_lv2_nameen": "ABI",
        "normal_list": [
            "nodetectableabnormality",
            "noabnormality"
        ],
        "borderline_list": [
            "ผิดปกติเล็กน้อย",
            "borderline"
        ],
        "abnormal_list": [
            "abnormalstudy"
        ],
        "notexamined_list": [
            "ไม่ตรวจ",
            "ไม่มีผลตรวจ",
            "ไม่เข้ารับการตรวจ",
            "ปฏิเสธการตรวจ",
            "ปฏิเสธตรวจ"
        ]
    }
]
```

- db: ocare_cda, collection: model_expert_L2_recommend_dict, document: list of lv2 items

Tasks

CRUD item in:
- collection
- document: selected item_lv2_nameen; ie. diseasecapture,detail,interpret

--- in diseasecapture CRUD dict item 

----- name: CRUD th, en

----- definition : CRUD disease, risk, nodiseae

----- assessment: CRUD item in dict of disease, risk, nodisease

--- in detail CRUD dict item 

----- in each item consists of (undefined,notexamined,abnormal,normal in th, en)

--- in interpret CRUD dict item 

----- in each item consists of (undefined,notexamined,abnormal,normal in th, en)

```
[
{
	"item_lv2_NameEn": "Fasting Blood Sugar",
	"diseasecapture": {
		"Diabetes": {
			"name": {
				"th": "โรคเบาหวาน",
				"en": "Diabetes"
			},
			"definition": {
				"disease": "เป็นโรคเบาหวาน",
				"risk": "เสี่ยงโรคเบาหวาน",
				"nodisease": "ไม่พบภาวะเบาหวาน"
			},
			"assessment": {
				"disease": {
					"FBS": ["สูงกว่าปกติ", "สูง"],
					"DTX": ["สูงกว่าปกติ", "สูง"],
					"Estimated": ["สูงกว่าปกติ", "สูง"],
					"HbA1C": ["สูงกว่าปกติ", "สูง"]
				},
				"risk": {
					"FBS": ["เริ่มสูง"],
					"DTX": ["เริ่มสูง"],
					"Estimated": ["เริ่มสูง"],
					"HbA1C": ["เริ่มสูง"]
				},
				"nodisease": {
					"FBS": ["ปกติ", "ต่ำกว่าปกติ"],
					"DTX": ["ปกติ", "ต่ำกว่าปกติ"],
					"Estimated": ["ปกติ"],
					"HbA1C": ["ปกติ", "ต่ำกว่าปกติ"]
				}
			},
			"ref": ""
		}
	},
	"detail": {
		"diabetes": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "อาจจะมีภาวะเบาหวาน (Diabetes) </br>&nbsp; &nbsp; ควรปรึกษาแพทย์เพื่อตรวจเพิ่มเติมควรปรึกษาแพทย์เพื่อจะไน 5 ครั้งต่อสัปดาห์ (เช่น การเดินเร็ว) ",
				"en": "High blood sugar than normal (in the Diabetes category), you should consult your doctor to maal activities that fit at least 30 minutes a day, five times a week (for example, brisk walking)."
			},
			"normal": {
				"th": "",
				"en": ""
			}
		},
		"ifg": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "อยู่ในกลุ่มเสี่ยงเบาหวาน (Pre-diabetes) </br>&nbsp; &nbsp; ควรปรับเปลี่ยนพฤติกรรมการรับประทานอาหาร โดยลดอาหารประย่างต่อเนื่องอย่างน้อยปีละ 1 ครั้ง ",
				"en": "Higher than normal blood sugar levels (Pre-diabetes). Should change dietary habits bnt options and for ongoing monitoring at least 1 year."
			},
			"normal": {
				"th": "",
				"en": ""
			}
		},
		"hypoglycemia": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": " หากมีอาการผิดปกติ เช่น ใจสั่น มึนงง หน้ามืด ควรปรึกษาแพสมต่อไป",
				"en": "Blood sugassess and continue to provide appropriate treatment."
			},
			"normal": {
				"th": "",
				"en": ""
			}
		},
		"bloodsugar": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "",
				"en": ""
			},
			"normal": {
				"th": "",
				"en": ""
			}
		}
	},
	"interpret": {
		"diabetes": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "ระดับน้ำตาลในเลือดอยู่ในเกณฑ์ผิดปกติ อยู่ในเกณฑ์เบาหวาน (Diabetes) ควรปรึกษาแพทย์เพื่อตรวจเพิ่มเติม",
				"en": "Sugar levels in the blood are in the abnormal range."
			},
			"normal": {
				"th": "",
				"en": ""
			}
		},
		"ifg": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "ระดับน้ำตาลในเลือดอยู่ในเกณฑ์ผิดปกติ อยู่ในกลุ่มเสี่ยงเบาหวาน (Pre-diabetes) ควรปรึกษาแพทย์เพื่อตรวจเพิ่มเติม",
				"en": "Higher than normal blood sugar levels (Pre-diabetes). "
			},
			"normal": {
				"th": "",
				"en": ""
			}
		},
		"bloodsugar": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "",
				"en": ""
			},
			"normal": {
				"th": "ระดับน้ำตาลในเลือดอยู่ในเกณฑ์ปกติ",
				"en": "Normal blood sugar  "
			}
		},
		"hypoglycemia": {
			"undefined": {
				"th": "",
				"en": ""
			},
			"notexamined": {
				"th": "",
				"en": ""
			},
			"abnormal": {
				"th": "ระดับน้ำตาลในเลือดอยู่ในเกณฑ์ต่ำกว่าปกติ",
				"en": "Low blood sugar  "
			},
			"normal": {
				"th": "",
				"en": ""
			}
		}
	}
}
]
```

- db: ocare_cda, collection: model_expert_L3_ref, document: list of items with tag item_lv3_NameEn

Tasks

CRUD item in:
- collection
- document: selected item_lv3_nameen; ie. min max (m/ f),itp,define, assess, stage, unit, normal, dict (th/ en)

```
[
    {
        "item_lv3_NameEn":"ABI",
        "item": {
            "priority": {
                "set": "abnormalfirst",
                "nlp": {'enable':'1',
                            'path':'c:/services/serv-expert/app/',
                            'modelname':'abi',
                            'model_list':['abi','abivalue','elasticity']}
            },
            "min3": {
                "m": "",
                "f": ""
            },
            "min2": {
                "m": "",
                "f": ""
            },
            "min1": {
                "m": "",
                "f": ""
            },
            "min": {"m": "", "f": ""},
            "max3": {
                "m": "",
                "f": ""
            },
            "max2": {
                "m": "",
                "f": ""
            },
            "max1": {
                "m": "",
                "f": ""
            },
            "max": {"m": "", "f": ""},
            "tmin": {"m": "", "f": ""},
            "tmax": {"m": "", "f": ""},
            "itp": {
                "normal": "",
                "abnormal": "",
                "borderline": "",
                "over3": "",
                "over2": "",
                "over1": "",
                "over": "",
                "overt": "",
                                "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "",
                "undert": ""
            },
            "define": {
                "normal": "normal",
                "abnormal": "",
                "borderline": "normal",
                "over3": "",
                "over2": "",
                "over1": "",
                "over": "normal",
                "overt": "normal",
                                "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "abnormal",
                "undert": "abnormal"
            },
            "assess": {
                "normal": "",
                "abnormal": "",
                "borderline": "",
                "over3": "",
                "over2": "",
                "over1": "",
                "over": "",
                "overt": "",
                                "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "",
                "undert": ""
            },
            "stage":  {
                "normal": "",
                "abnormal": "",
                "borderline": "",
                "over3": "",
                "over2": "",
                "over1": "",
                "over": "",
                "overt": "",
                                "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "",
                "undert": ""
            },
            "unit": "",
            "normal": "",
            "dict": {
                "th": {
                                    "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "",
                    "undert": "",
                    "over3": "",
                "over2": "",
                "over1": "",
                "over": "",
                    "overt": "",
                    "borderline": "ผลการตรวจสมรรถภาพการไหลเวียนของเส้นเลือด (ABI) โดยเปรียบเทียบความดันโลหิตระหว่างหลอดเลือดแดงที่แขน (Brachial Artery) และหลอดเลือดแดงที่ขาบริเวณข้อเท้า (Ankle) ก้ำกึ่งผิดปกติ",
                    "normal": "ผลการตรวจสมรรถภาพการไหลเวียนของเส้นเลือด (ABI) โดยเปรียบเทียบความดันโลหิตระหว่างหลอดเลือดแดงที่แขน (Brachial Artery) และหลอดเลือดแดงที่ขาบริเวณข้อเท้า (Ankle) ปกติ",
                    "abnormal": "ผลการตรวจสมรรถภาพการไหลเวียนของเส้นเลือด (ABI) โดยเปรียบเทียบความดันโลหิตระหว่างหลอดเลือดแดงที่แขน (Brachial Artery) และหลอดเลือดแดงที่ขาบริเวณข้อเท้า (Ankle) พบความผิดปกติ",
                    "notexamined": "",
                    "undefined": "",
                },
                "en": {
                                    "under3": "",
                    "under2": "",
                    "under1": "",
                    "under": "",
                    "undert": "",
                    "over3": "",
                "over2": "",
                "over1": "",
                "over": "",
                    "overt": "",
                    "borderline": "The results of the blood flow function test (ABI) were slightly abnormal.",
                    "normal": "The results of the blood flow function test (ABI) were normal.",
                    "abnormal": "The results of the blood flow function (ABI) test revealed abnormalities. It is recommended to consult a doctor. for further examination",
                    "notexamined": "",
                    "undefined": "",
                }
            }
        }
    }
]
```

### 3. CDA-model-ml

- as collection schema
-  db: ocare_cda, collection: model_ml, document: list of items with tag item_lv3_NameEn

Tasks

CRUD item in:
- collection
- document: selected item_lv3_nameen; ie. label, label_name, group, category_codes, column

```
[{
		"item_lv3_NameEn": "Chest X-Ray",
		"label": "cxr","label_name": {"th":"label_th","en":"label_en"},"group": "chest","category_codes": {
			"0": "0",
			"1": "1",
			"9": "9",
			"10": "10"
		},
		"column": "interpret"
	},
	{
		"item_lv3_NameEn": "Chest X-Ray",
		"label": "heart","label_name": {"th":"label_th","en":"label_en"},"group": "chest","category_codes": {
			"0": "0",
			"1": "1",
			"9": "9",
			"10": "10"
		},
		"column": "heart"
	}]
```

### 4. CDA-model-clinical
- (done) call model from NoSQLDB
- db: ocare_cda, collection: model_clinical, document: list of items with tag item_lv3_NameEn

Tasks

CRUD item in:
- collection
- document: selected item_lv3_nameen (item); ie. active, logictype, logic: string/ nlp/ numeric

```
{
	"item": "Hemoglobin",
	"active": "FALSE",
	"logictype": {
		"string":"FALSE",
		"numeric":"TRUE",
		"nlp":"FALSE"
	},
	"logic": {
		"string": {
			"model": [{
				"model_label": {"TH":"ภาวะซีด","EN":"anemia"},
				"group": "hemato",
				"exactmatch": "TRUE",
				"normal": ["ddd"],
				"abnormal": ["sss"],
				"borderline": ["ddd"],
				"undefined": ["dd"]
			}, {
				"model_label": {"TH":"เลือดเข้ม","EN":"polycythemia"},
				"group": "hemato",
				"exactmatch": "FALSE",
				"normal": ["ddd"],
				"abnormal": ["sss"],
				"borderline": ["ddd"],
				"undefined": ["dd"]
			}]
		},
		"nlp": {
			"model": ["anemia", "polycythemia"]
		},
		"numeric": {
			"model": [{
					"model_label": {"TH":"ภาวะซีด","EN":"anemia"},
					"group": "hemato",
					"overt": "",
					"over": "",
					"under": "TRUE",
					"undert": ""
				},
				{
					"model_label": {"TH":"เลือดข้น","EN":"polycythemia"},
					"group": "hemato",
					"overt": "",
					"over": "TRUE",
					"under": "",
					"undert": ""
				}
			],
			"value": {
				"tmax": "20",
				"max": "18",
				"min": "14",
				"tmin": "13"
			}
		}
	}
}
```
