# Local ECG image dataset

Use `data/ecg_report_images/` as the default dataset location. The notebook checks direct child folder names, case-insensitively, for these phrases:

| Required phrase in folder name | Assigned class |
| --- | --- |
| `abnormal heartbeat` | Abnormal_Heartbeat |
| `history of mi` | MI_history |
| `myocardial infarction` | Myocardial_Infarction |
| `normal` | Normal |

Example relative paths:

- `data/ecg_report_images/Abnormal Heartbeat/example.png`
- `data/ecg_report_images/History of MI/example.png`
- `data/ecg_report_images/Myocardial Infarction/example.png`
- `data/ecg_report_images/Normal/example.png`

Use those phrases with spaces. Names such as `Abnormal_Heartbeat` or `MI_history` do not match the supplied loader. Folders with unmatched names are skipped.

Each recognized class folder must contain readable image files directly, without nested folders or other files. The baseline does not filter extensions or handle unreadable images. Provide all four classes; the original one-hot encoding infers its width from the labels found.

Dataset images remain local and are excluded from Git. Record the original dataset source and license in the main README once verified.
