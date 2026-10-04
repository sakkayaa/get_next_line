# get_next_line

> **C ile dosyalardan satır satır okuma**
> Dosya tanımlayıcısından bir satır okuyan ve her çağrıda sonraki satırı döndüren bir C projesi.

## Proje hakkında

`get_next_line`, açık bir dosya tanımlayıcısından (`fd`) veriyi okur ve her çağrıda bir sonraki satırı dinamik olarak ayrılmış bir string olarak döndürür. Satır sonu (`\n`) varsa dönen satıra dahildir. Dosyanın sonuna gelindiğinde veya okuma başarısız olduğunda fonksiyon `NULL` döndürür.

Proje; `read`, statik değişkenler, dinamik bellek yönetimi, buffer kullanımı ve dosya tanımlayıcılarıyla çalışma konularını kapsar. Harici kütüphane bağımlılığı yoktur.

## Öne çıkanlar

- **Satır satır okuma:** her çağrıda bir satır döndürür
- **Ayarlanabilir buffer:** `BUFFER_SIZE` derleme sırasında belirlenebilir
- **Dinamik bellek:** satırlar ve kalan veri için bellek yönetimi
- **Bonus sürüm:** birden fazla dosya tanımlayıcısı için ayrı okuma durumu
- **C ve POSIX dosya işlemleri:** `read`, `open` ve `close`

## Dosyalar

| Dosya | Amaç |
|---|---|
| `get_next_line.c` | Temel sürümün satır okuma fonksiyonu |
| `get_next_line_utils.c` | Temel sürümün string ve satır yardımcıları |
| `get_next_line.h` | Temel sürümün tanımları ve bildirimleri |
| `get_next_line_bonus.c` | Birden fazla dosya tanımlayıcısını destekleyen bonus sürüm |
| `get_next_line_utils_bonus.c` | Bonus sürümün yardımcı fonksiyonları |
| `get_next_line_bonus.h` | Bonus sürümün tanımları ve bildirimleri |

## Gereksinimler

- C derleyicisi (`cc`, `gcc` veya uyumlu bir derleyici)
- POSIX uyumlu işletim sistemi

## Derleme ve kullanım

Projede Makefile bulunmadığından kaynak dosyalarını derleyiciye doğrudan verin. Aşağıdaki örnekte `main.c`, `get_next_line` fonksiyonunu kullanan programınızdır.

Temel sürüm:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  main.c get_next_line.c get_next_line_utils.c -o gnl
```

Bonus sürüm:

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 \
  main.c get_next_line_bonus.c get_next_line_utils_bonus.c -o gnl
```

Örnek kullanım:

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main(void)
{
    int fd = open("input.txt", O_RDONLY);
    char *line;

    if (fd < 0)
        return (1);
    while ((line = get_next_line(fd)) != NULL)
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

`BUFFER_SIZE` değeri her `read` çağrısında okunacak bayt sayısını belirler. Farklı değerlerle derleyerek buffer boyutunun okuma davranışına etkisini inceleyebilirsiniz.

## Öğrenme çıktıları

Bu çalışma; dosya I/O, buffer yönetimi, statik değişkenler, dinamik bellek ayırma ve birden fazla dosya tanımlayıcısı için durum tutma becerilerini gösterir.

## Geliştiren

**Sedef Akkaya**
GitHub: [sakkayaa](https://github.com/sakkayaa) · LinkedIn: [Sedef Akkaya](https://www.linkedin.com/in/sedef-akkaya-0a5580228/)

---

*Her çağrıda bir satır. Dosyanın sonuna kadar.*
