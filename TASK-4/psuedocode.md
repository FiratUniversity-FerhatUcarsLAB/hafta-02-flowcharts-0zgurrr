BAŞLA

// 1. Öğrenci girişi
OGR_NO = GİR("Öğrenci numaranızı giriniz: ")
SIFRE = GİR("Şifrenizi giriniz: ")

EĞER GIRIŞ_DOĞRU_MU(OGR_NO, SIFRE) DEĞİLSE
    YAZDIR("Hatalı giriş. Sistemden çıkılıyor.")
    BİTİR
SON
YAZDIR("Giriş başarılı.")

// 2. Ders listesi ve seçim döngüsü
DÖNGÜ:
    DERS_LISTESI = GÖSTER_DERSLER()
    SEÇİM = GİR("Ders seçin veya çıkarmak için numara girin: ")

    // Kontenjan kontrolü
    EĞER KONTENJAN_VAR_MI(SEÇİM) DEĞİLSE
        YAZDIR("Kontenjan dolu, başka ders seçin.")
        GİT DÖNGÜ BAŞI
    SON

    // Ön koşul kontrolü
    EĞER ÖN_KOŞUL_TAMAM_MI(SEÇİM) DEĞİLSE
        YAZDIR("Ön koşul derslerini tamamlamanız gerekiyor.")
        GİT DÖNGÜ BAŞI
    SON

    // Zaman çakışması kontrolü
    EĞER ZAMAN_CAKISIYOR_MU(SEÇİM) İSE
        YAZDIR("Seçilen ders zaman çakışıyor.")
        GİT DÖNGÜ BAŞI
    SON

    // Kredi limiti kontrolü
    EĞER TOPLAM_KREDI + DERS_KREDISI(SEÇİM) > 35 İSE
        YAZDIR("Toplam kredi limiti aşılıyor.")
        GİT DÖNGÜ BAŞI
    SON

    // Ders ekleme
    DERS_EKLE(SEÇİM)
    YAZDIR("Ders eklendi.")

    // Ders çıkarma
    CEVAP = GİR("Ders çıkarmak ister misiniz? (E/H): ")
    EĞER CEVAP == "E" İSE
        DERS = GİR("Çıkarmak istediğiniz ders: ")
        DERS_CIKAR(DERS)
    SON

    // Danışman onayı kontrolü
    EĞER DANISMAN_ONAYI_GEREKLI_MI() İSE
        YAZDIR("Danışman onayı gerekiyor.")
        ONAY_AL()
    SON

    // Başka ders seçimi
    CEVAP2 = GİR("Başka ders seçmek ister misiniz? (E/H): ")
    EĞER CEVAP2 == "E" İSE
        GİT DÖNGÜ BAŞI
    DEĞİLSE
        BREAK
SON

// 3. Kayıt özeti ve onay
YAZDIR("Kayıt özeti:")
GÖSTER_KAYIT_OZETI()
CEVAP3 = GİR("Kaydı onaylıyor musunuz? (E/H): ")
EĞER CEVAP3 == "E" İSE
    YAZDIR("Kayıt onaylandı.")
DEĞİLSE
    YAZDIR("Kayıt onayı iptal edildi.")

BİTİR
