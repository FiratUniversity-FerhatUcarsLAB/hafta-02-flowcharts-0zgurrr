BAŞLA

// 1. Sistem durumu kontrolü
EĞER SISTEM_AKTIF_MI() DEĞİLSE
    YAZDIR("Güvenlik sistemi kapalı.")
    BİTİR
SON

// 2. Ana döngü – sürekli sensör kontrolü
DÖNGÜ: // 7/24 sürekli çalışacak
    // Sensörleri oku
    HAREKET = HAREKET_SENSOR_OKU()
    KAPI = KAPI_SENSOR_OKU()
    PENCERE = PENCERE_SENSOR_OKU()
    KAMERA = KAMERA_SENSOR_OKU()

    // Tehdit kontrolü
    TEHDIT = HAREKET_VEYA_KAPI_PENCERE_ALERT(HAREKET, KAPI, PENCERE)

    EĞER TEHDIT == HAYIR DEĞİLSE
        // Yanlış alarm kontrolü
        EĞER EV_SAHIBI_EVDE_MI() İSE
            YAZDIR("Yanlış alarm: Ev sahibi evde.")
        DEĞİLSE
            // Alarm seviyesi belirleme
            SEVİYE = ALARM_SEVIYESI_BELIRLE(TEHDIT)
            YAZDIR("Alarm seviyesi: ", SEVİYE)

            // Alarm ve bildirim gönder
            ALARM_VER(SEVİYE)
            BILDIRIM_GONDER("SMS + App + Email", SEVİYE)
        SON
    SON

    // Bekle ve tekrar kontrol et
    BEKLE(1 saniye)
SON

// 3. Alarm sıfırlama veya devam ettirme (opsiyonel)
EĞER ALARM_SIFIRLA_DEGIL_MI() İSE
    BIRAK DÖNGÜ
SON

BİTİR
