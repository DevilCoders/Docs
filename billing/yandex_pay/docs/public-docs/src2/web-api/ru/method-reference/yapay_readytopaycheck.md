# YaPay.readyToPayCheck

YaPay.readyToPayCheck — метод, проверяющий доступность {{ product }} для оплаты.



### **Конструктор** {#constructor}
Функция-конструктор. На основе переданных параметров проверяет возможность получить платежный токен.
Проверяется:
- ` merchantId `;
- возможность генерации токена по указанным платежным данным (опционально).



```
{Promise<boolean>} readyToPayCheck(params)
```

**Параметры:**
| **Название** | **Тип** | **Описание** | **По умолчанию** |
| --- | --- | --- | --- |
| `options` | [ReadyToPayCheckParams](yapay.md#ready-to-pay-check-params) | Опции, проверяющие возможность получения токена. | — |

