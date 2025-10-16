```
BAŞLA

KART_TAK()

PIN_DENEME = 0

TEKRAR:
    PIN = PIN_GİR()
    EĞER PIN_DOĞRU(PIN) İSE
        GİT BAKİYE_SORGULA
    DEĞİLSE
        PIN_DENEME = PIN_DENEME + 1
        EĞER PIN_DENEME >= 3 İSE
            YAZDIR("Kart bloke oldu. Lütfen banka ile iletişime geçin.")
            KARTI_İADE_ET()
            BİTİR
        DEĞİLSE
            YAZDIR("Yanlış PIN, tekrar deneyin.")
            GİT TEKRAR
        SON
    SON

BAKİYE_SORGULA:
    BAKİYE = BAKİYE_ÖĞREN()
    YAZDIR("Mevcut bakiyeniz: ", BAKİYE, " TL")

    TUTAR_GİR:
        ÇEKİLECEK_TUTAR = TUTAR_GİRİŞİ()
        
        EĞER ÇEKİLECEK_TUTAR % 20 != 0 İSE
            YAZDIR("Tutar 20 TL'nin katı olmalı.")
            GİT TUTAR_GİR
        SON
        
        EĞER ÇEKİLECEK_TUTAR > GÜNLÜK_LIMIT İSE
            YAZDIR("Günlük limit aşıldı.")
            GİT TUTAR_GİR
        SON
        
        EĞER ÇEKİLECEK_TUTAR > BAKİYE İSE
            YAZDIR("Yetersiz bakiye.")
            GİT TUTAR_GİR
        SON
        
        PARA_VER(ÇEKİLECEK_TUTAR)
        BAKİYE = BAKİYE - ÇEKİLECEK_TUTAR
        MAKBUZ_YAZDIR()
        
        YAZDIR("İşlem başarılı. Kalan bakiye: ", BAKİYE, " TL")

        BAŞKA_İŞLEM = SOR("Başka işlem yapmak ister misiniz? (E/H): ")
        EĞER BAŞKA_İŞLEM == "E" İSE
            GİT BAKİYE_SORGULA
        DEĞİLSE
            KARTI_İADE_ET()
            YAZDIR("Teşekkürler, iyi günler.")
            BİTİR
        SON

    ```
