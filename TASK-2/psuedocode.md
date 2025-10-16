digraph Online_Alisveris_Sepet_Sistemi {
    rankdir=TB;
    node [fontname="Arial", fontsize=10, style=filled, fillcolor=white];

    start [shape=ellipse, label="Başla"];

    giris_sor [shape=parallelogram, label="Giriş yapmak ister misiniz? (E/H)"];
    giris_kontrol [shape=diamond, label="Kullanıcı giriş yaptı mı?"];
    giris_bitis [shape=ellipse, label="Bitir"];
    
    kategori_gezin [shape=box, label="Kategoriler arasında gezin"];
    urun_sec [shape=parallelogram, label="Ürün seç ve miktar gir"];
    stok_kontrol [shape=diamond, label="Stokta var mı?"];
    stok_yok [shape=parallelogram, label="Stokta yok!"];
    sepete_ekle [shape=box, label="Ürünü sepete ekle"];
    tekrar_urun [shape=diamond, label="Başka ürün eklemek istiyor mu?"];
    
    sepet_gor [shape=parallelogram, label="Sepeti görüntüle"];
    sepet_duzenle [shape=diamond, label="Sepeti düzenlemek istiyor mu?"];
    urun_sil [shape=box, label="Ürünü sepetten kaldır"];
    
    indirim_sor [shape=diamond, label="İndirim kodu var mı?"];
    indirim_kontrol [shape=diamond, label="Kod geçerli mi?"];
    indirim_uygula [shape=box, label="İndirimi uygula"];
    
    min_tutar [shape=diamond, label="Toplam < 50 TL mi?"];
    kargo_kontrol [shape=diamond, label="Toplam >= 200 TL mi?"];
    kargo_ucretsiz [shape=box, label="Kargo ücretsiz"];
    kargo_ucretli [shape=box, label="Kargo ücreti 30 TL ekle"];
    
    odeme_sec [shape=parallelogram, label="Ödeme yöntemi seç (1/2/3)"];
    odeme_kontrol [shape=diamond, label="Geçerli ödeme yöntemi mi?"];
    siparis_onay [shape=box, label="Sipariş onayla"];
    odeme_hata [shape=parallelogram, label="Geçersiz seçim! İşlem iptal."];
    end [shape=ellipse, label="Bitir"];

    // Bağlantılar
    start -> giris_sor -> giris_kontrol;
    giris_kontrol -> giris_bitis [label="H"];
    giris_kontrol -> kategori_gezin [label="E"];
    
    kategori_gezin -> urun_sec -> stok_kontrol;
    stok_kontrol -> stok_yok [label="Hayır"];
    stok_kontrol -> sepete_ekle [label="Evet"];
    stok_yok -> tekrar_urun;
    sepete_ekle -> tekrar_urun;
    
    tekrar_urun -> kategori_gezin [label="Evet"];
    tekrar_urun -> sepet_gor [label="Hayır"];
    
    sepet_gor -> sepet_duzenle;
    sepet_duzenle -> urun_sil [label="Evet"];
    urun_sil -> sepet_gor;
    sepet_duzenle -> indirim_sor [label="Hayır"];
    
    indirim_sor -> indirim_kontrol [label="Evet"];
    indirim_sor -> min_tutar [label="Hayır"];
    indirim_kontrol -> indirim_uygula [label="Geçerli"];
    indirim_kontrol -> min_tutar [label="Geçersiz"];
    indirim_uygula -> min_tutar;

    min_tutar -> giris_bitis [label="Evet"];
    min_tutar -> kargo_kontrol [label="Hayır"];
    
    kargo_kontrol -> kargo_ucretsiz [label="Evet"];
    kargo_kontrol -> kargo_ucretli [label="Hayır"];
    kargo_ucretsiz -> odeme_sec;
    kargo_ucretli -> odeme_sec;

    odeme_sec -> odeme_kontrol;
    odeme_kontrol -> siparis_onay [label="Evet"];
    odeme_kontrol -> odeme_hata [label="Hayır"];
    siparis_onay -> end;
    odeme_hata -> end;
}
