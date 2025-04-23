## Generate file list for FROM_SANDBOX macro 

```bash
find result/ -type f | grep -v share | python3 -c "import sys;[print('  RENAME result/{} OUT_NOAUTO {}'.format(line, line)) for line in (line.strip()[len('result/'):] for line in sys.stdin)]" | sort
```
