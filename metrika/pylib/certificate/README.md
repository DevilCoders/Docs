```python
import metrika.pylib.certificate


if __name__ == '__main__':
    cert = metrika.pylib.certificate.Certificate(filanem='certificate.pem')
    start_date, end_date = cert.get_dates()

    print('Certificate dates: from {} to {}'.format(start_date, end_date))

    valid, errors = cert.is_valid()

    if not valid:
        print('Certificate is not valid: {}'.formata(', '.join(errors)))
    else:
        print('Certificate is valid')
```
