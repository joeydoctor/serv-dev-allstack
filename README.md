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
- convert var .py to json
- link json library (L2, library) to NoSQLDB

- db: ocare_cda, collection: model_expert_list_normal, document: list of items with tag item_lv2_NameEn

Tasks

 CRUD item in: 
- collection
- document: item, selected item_lv2_nameen

```
[{
	"item_lv2_nameen": "Cervical Cancer Screening",
	"normal_list": [
		"normal",
		"ปกติ",
		"unremarkable",
		"notfound",
		"adequate",
		"negative",
		"negativeforintraepitheliallesionormalignancy"
	]
}]
```

- db: ocare_cda, collection: model_expert_list_abnormal, document: list of items with tag item_lv2_NameEn

Tasks

 CRUD item in: 
- collection
- document: item, selected item_lv2_nameen

```
[{
	"item_lv2_NameEn": "Cervical Cancer Screening",
	"abnormal_list": [
		"abnormal",
		"ผิดปกติ",
		"positive",
		"พบเชลล์ผิดปกติควรพบแพทย์เพื่อวินิจฉัยเพิ่มเติม"
	]
}]
```
- db: ocare_cda, collection: model_expert_list_borderline, document: list of items with tag item_lv2_NameEn

Tasks

 CRUD item in: 
- collection
- document: item, selected item_lv2_nameen

```
[{
	"item_lv2_NameEn": "Cervical Cancer Screening",
	"borderline_list": [
		"ผิดปกติเล็กน้อย",
		"borderline"
	]
}]
```
- db: ocare_cda, collection: model_expert_list_notexamined, document: list of items with tag item_lv2_NameEn

Tasks

CRUD item in: 
- collection
- document: item, selected item_lv2_nameen

```
[{
	"item_lv2_NameEn": "Cervical Cancer Screening",
	"notexamined_list": [
		"ไม่ตรวจ",
		"ไม่มีผล",
		"ไม่มีผลตรวจ",
		"รอผลตรวจ",
		"ไม่เข้ารับการตรวจ",
		"ปฏิเสธการเจาะเลือด",
		"ปฏิเสธตรวจ"
	]
}]
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
[{
	{
    "FBS": {
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
        "min": {
            "m": "70",
            "f": "70"
        },
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
        "max": {
            "m": "110",
            "f": "110"
        },
        "tmin": {
            "m": "",
            "f": ""
        },
        "tmax": {
            "m": "126",
            "f": "126"
        },
        "itp": {
            "normal": "",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "",
            "overt": "เริ่มสูง",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "",
            "undert": ""
        },
        "define": {
            "normal": "",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "",
            "overt": "abnormal",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "",
            "undert": ""
        },
        "assess": {
            "normal": "น้ำตาลปกติ",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "มีภาวะเบาหวาน",
            "overt": "เสี่ยงเบาหวาน",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "น้ำตาลต่ำ",
            "undert": ""
        },
        "stage":  {
            "normal": "0",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "2",
            "overt": "1",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "-1",
            "undert": ""
        },
        "unit": "mg/dL",
        "normal": "",
        "dict": {
            "th": {
                                "under3": "",
                "under2": "",
                "under1": "",
                "under": "ระดับน้ำตาลในเลือดต่ำกว่าเกณฑ์ปกติ",
                "undert": "",
                "over3": "",
            "over2": "",
            "over1": "",
            "over": "ระดับน้ำตาลในเลือดสูงกว่าเกณฑ์ปกติ",
                "overt": "ระดับน้ำตาลในเลือดสูงกว่าเกณฑ์ปกติ",
                "borderline": "",
                "normal": "ระดับน้ำตาลในเลือดอยู่ในเกณฑ์ปกติ",
                "abnormal": "",
                "notexamined": "",
                "undefined": ""
            },
            "en": {
                                 "under3": "",
                 "under2": "",
                 "under1": "",
                 "under": "The blood sugar level is below normal",
                 "undert": "",
                 "over3": "",
             "over2": "",
             "over1": "",
             "over": "The blood sugar level is above normal",
                 "overt": "The blood sugar level is above normal",
                 "borderline": "",
                 "normal": "The blood sugar level is normal",
                 "abnormal": "",
                 "notexamined": "",
                 "undefined": ""
             }
        }
    }
    },
    {
    "DTX": {
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
        "min": {
            "m": "70",
            "f": "70"
        },
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
        "max": {
            "m": "110",
            "f": "110"
        },
        "tmin": {
            "m": "",
            "f": ""
        },
        "tmax": {
            "m": "126",
            "f": "126"
        },
        "itp": {
            "normal": "",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "",
            "overt": "เริ่มสูง",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "",
            "undert": ""
        },
        "define": {
            "normal": "",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "",
            "overt": "abnormal",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "",
            "undert": ""
        },
        "assess": {
            "normal": "น้ำตาลปกติ",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "มีภาวะเบาหวาน",
            "overt": "เสี่ยงเบาหวาน",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "น้ำตาลต่ำ",
            "undert": ""
        },
        "stage":  {
            "normal": "0",
            "abnormal": "",
            "borderline": "",
            "over3": "",
            "over2": "",
            "over1": "",
            "over": "2",
            "overt": "1",
                            "under3": "",
                "under2": "",
                "under1": "",
                "under": "-1",
            "undert": ""
        },
        "unit": "mg/dL",
        "normal": "",
        "dict": {
            "th": {
                                "under3": "",
                "under2": "",
                "under1": "",
                "under": "ระดับน้ำตาลในเลือดปลายนิ้วต่ำกว่าเกณฑ์ปกติ",
                "undert": "",
                "over3": "",
            "over2": "",
            "over1": "",
            "over": "ระดับน้ำตาลในเลือดปลายนิ้วสูงกว่าเกณฑ์ปกติ",
                "overt": "ระดับน้ำตาลในเลือดปลายนิ้วสูงกว่าเกณฑ์ปกติ",
                "borderline": "",
                "normal": "ระดับน้ำตาลในเลือดปลายนิ้วอยู่ในเกณฑ์ปกติ",
                "abnormal": "",
                "notexamined": "",
                "undefined": ""
            },
            "en": {
                                 "under3": "",
                 "under2": "",
                 "under1": "",
                 "under": "The fingertip blood sugar level is below normal",
                 "undert": "",
                 "over3": "",
             "over2": "",
             "over1": "",
             "over": "The fingertip blood sugar level is higher than normal.",
                 "overt": "fingertip blood sugar levels are above normal",
                 "borderline": "",
                 "normal": "The fingertip blood sugar level is normal.",
                 "abnormal": "",
                 "notexamined": "",
                 "undefined": ""
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
