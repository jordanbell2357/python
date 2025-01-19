# json

```python
# csv_to_json.py

import csv
import json

INPUT_FILE_PATH = 'name.basics.tsv'
OUTPUT_FILE_PATH = 'name.basics.json'

with open(INPUT_FILE_PATH, 'r', encoding='utf-8') as tsv_file:
    csv_reader = csv.DictReader(tsv_file, delimiter='\t')
    with open(OUTPUT_FILE_PATH, 'w', encoding='utf-8') as json_file:
        json_file.write('[\n')  # Start the JSON array

        header_row = next(csv_reader)
        if header_row:
            json.dump(header_row, json_file, separators=(',', ':'), ensure_ascii=False)

            for row in csv_reader:
                json_file.write(',\n')  # Add a comma and newline before each subsequent row
                row_dict = {k: (None if v == r'\N' else v) for k, v in row.items()}
                row_dict['birthYear'] = int(row_dict['birthYear']) if row_dict['birthYear'] else None
                row_dict['deathYear'] = int(row_dict['deathYear']) if row_dict['deathYear'] else None
                json.dump(row_dict, json_file, separators=(',', ':'), ensure_ascii=False)

        json_file.write('\n]\n')  # End the JSON array
```

```bash
head -n 2 name.basics.json
# [
# {"nconst":"nm0000001","primaryName":"Fred Astaire","birthYear":"1899","deathYear":"1987","primaryProfession":"actor,miscellaneous,producer","knownForTitles":"tt0072308,tt0050419,tt0053137,tt0027125"},
```

```bash
tail -n 2 name.basics.json
# {"nconst":"nm9993719","primaryName":"Andre Hill","birthYear":null,"deathYear":null,"primaryProfession":null,"knownForTitles":null}
# ]
```
