# Lab 5 Issues Table

Student: Aman Priyansh (PES1UG24AM030)
File: electricity_bill.py

Scores: Pylint 5.44 -> 10.00, Bandit 4 issues -> 0, Flake8 4 issues -> 0.
The program prints exactly the same output before and after (four bills, highest bill M2, average 934.5, total 3738.0).
The before and after tool reports are in the repository root (pylint_report_before.txt, pylint_report_after.txt, and so on).

Line numbers refer to the ORIGINAL file.

| Issue | Type | Line(s) | Description | Fix Approach |
|-------|------|---------|-------------|--------------|
| Shell command built from a string (B605, High) | Security | 63 | os.system("curl http://" + meterIp + ...) puts an input value into a shell command, so a value like "1.2.3.4; rm -rf ~" runs extra commands (command injection, CWE-78). | Removed os.system. Validate the value with ipaddress.ip_address, then use http.client.HTTPConnection with a timeout. No shell is involved. |
| Untrusted XML parsing (B314, Medium; B405, Low) | Security | 3, 18 | xml.etree.ElementTree is vulnerable to XML attacks such as entity expansion when the XML comes from outside. | Replaced it with defusedxml.ElementTree (added requirements.txt). |
| Hardcoded password (B105, Low) | Security | 13 | CLERK_PASSWORD = "bill-desk-demo" is a secret stored in source code. It was never used. | Deleted the unused constant. If a password is needed later it should come from an environment variable. |
| Mutable default argument (W0102) | Bug | 42 | extras={} is created once and shared by every call, so a change inside the function would leak into later calls. | Default changed to None; a new dict is created inside the function. |
| Unused argument (W0613) | Code quality | 50 | averageBill(currency) never used currency. | Removed the parameter and updated the call in main(). |
| open() without encoding (W1514) | Portability | 57 | The file encoding depends on the operating system. | Added encoding="utf-8". |
| Naming style (C0103, many) | Style | 17-67 | camelCase function, argument and variable names do not follow PEP 8 snake_case. | Renamed all of them, e.g. readMeters -> read_meters, meterId -> meter_id. |
| Missing docstrings (C0114, C0116) | Documentation | 1, 17-66 | The module and every function had no docstring. | Added a short docstring to the module and each function. |
| main() runs on import | Design | 82 | main() was called at module level, so importing the file ran the whole demo. | Wrapped the call in if __name__ == "__main__". |
| Blank lines (E302) | Style | 22 | Only 1 blank line before a function; PEP 8 needs 2. | Added a blank line. |
| Space before colon (E203) | Style | 44 | "meter" : meterId | Removed the space. |
| Line too long (E501) | Style | 72 | 86 characters, limit is 79. | Split the print call over two lines. |
| Missing spaces around operator (E225) | Style | 76 | total=sum(...) | Changed to total = sum(...). |

## Commits

1. Fix Bandit issues (rows 1-3)
2. Fix Flake8 issues (last four rows)
3. Fix Pylint issues (rows 4-9)
