# git-scrape-unravel

CLI to unravel git-scraped code.

```python
# git-scrape-unravel
# filename = "foo.csv"

import json
from pydriller import RepositoryMining

for commit in RepositoryMining(".").traverse_commits():
    for modified_file in commit.modifications:
        if modified_file.new_path == "data.json":
            print(str(commit.author_date))
            dictionaries = [json.loads(s) for s in modified_file.source_code.split("\n") if len(s)]
            print([{"date": str(commit.author_date), **d} for d in dictionaries])
```
