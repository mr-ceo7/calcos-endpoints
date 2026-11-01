# calcos-endpoints

Where CalcOS calculators find their API when the address built into their firmware stops answering.

`endpoints.json` lists up to four API addresses, the first one preferred. It is signed with a key that never leaves the developer's machine, so a calculator ignores any list that was changed or signed by anyone else. Each list has a number (`seq`), and a calculator never goes back to a lower one.

Calculators read this file only after the API has not answered for six hours, and then once an hour. They send nothing to GitHub.

To publish a new list (in the casio-os repo):

```
tools/sign_endpoints.py sign --seq <higher than the last> https://api.new.example https://api.old.example
```

Commit the resulting `endpoints.json` here, and copy it to the API server as its `ENDPOINTS_FILE`.
