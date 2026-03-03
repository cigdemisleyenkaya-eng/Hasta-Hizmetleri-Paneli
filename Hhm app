import { useState, useEffect } from "react";

const RENKLER = {
  koyu: "#0A0F1E",
  panel: "#111827",
  kart: "#1a2235",
  sinir: "#1e3a5f",
  mavi: "#1d6fa4",
  acikMavi: "#38bdf8",
  yesil: "#10b981",
  sari: "#f59e0b",
  kirmizi: "#ef4444",
  turuncu: "#f97316",
  metin: "#e2e8f0",
  soluk: "#64748b",
};

const PERFORMANS_KRITERLERI = [
  { id: 1, kategori: "İletişim", baslik: "Hastayla İletişim", aciklama: "Hasta ile empati kurma ve açık iletişim" },
  { id: 2, kategori: "İletişim", baslik: "Yöneticiyle İletişim", aciklama: "Üst yönetimle etkin iletişim" },
  { id: 3, kategori: "İletişim", baslik: "Ekip İletişimi", aciklama: "Ekip arkadaşlarıyla işbirliği" },
  { id: 4, kategori: "Kişisel Özellikler", baslik: "Güleryüzlülük", aciklama: "Pozitif tutum ve güleryüzlü hizmet" },
  { id: 5, kategori: "Kişisel Özellikler", baslik: "İlgi & Empati", aciklama: "Hasta ihtiyaçlarına duyarlılık" },
  { id: 6, kategori: "Kişisel Özellikler", baslik: "Sabır & Sakinlik", aciklama: "Stresli durumlarda sakin kalma" },
  { id: 7, kategori: "Mesleki Yetkinlik", baslik: "Eğitim & Gelişim", aciklama: "Mesleki gelişime açıklık" },
  { id: 8, kategori: "Mesleki Yetkinlik", baslik: "Öğrenme Becerisi", aciklama: "Yeni bilgi ve becerileri edinme hızı" },
  { id: 9, kategori: "Mesleki Yetkinlik", baslik: "Teknik Yeterlilik", aciklama: "Mesleki teknik bilgi düzeyi" },
  { id: 10, kategori: "Liderlik", baslik: "İnisiyatif Alma", aciklama: "Sorunlara proaktif çözüm üretme" },
  { id: 11, kategori: "Liderlik", baslik: "Yetki Kullanımı", aciklama: "Sorumluluk alanında etkin karar alma" },
  { id: 12, kategori: "Liderlik", baslik: "Mentorluk", aciklama: "Yeni personele rehberlik etme" },
  { id: 13, kategori: "İş Performansı", baslik: "Zamanında Tamamlama", aciklama: "Görevleri zamanında bitirme" },
  { id: 14, kategori: "İş Performansı", baslik: "Kalite & Doğruluk", aciklama: "İş çıktısının kalitesi" },
  { id: 15, kategori: "İş Performansı", baslik: "Devam & Düzenlilik", aciklama: "Devam düzenliliği ve dakiklik" },
  { id: 16, kategori: "Uyum", baslik: "Kurumsal Kurallara Uyum", aciklama: "Hastane politika ve prosedürlerine uyum" },
  { id: 17, kategori: "Uyum", baslik: "Kıyafet & Hijyen", aciklama: "Kıyafet ve kişisel hijyen standartları" },
];

const BINA_KONUMLARI = ["Blok A - Zemin Kat", "Blok A - 1. Kat", "Blok A - 2. Kat", "Blok B - Zemin Kat", "Blok B - 1. Kat", "Blok C - Acil", "Blok C - Yoğun Bakım", "Klinik Bina", "İdari Bina"];
const BIRIMLER = ["Hasta Hizmetleri", "Acil Servis", "Dahiliye", "Cerrahi", "Ortopedi", "Kardiyoloji", "Pediatri", "Yoğun Bakım", "Radyoloji", "Laboratuvar"];
const UNVANLAR = ["Hasta Hizmetleri Uzmanı", "Kıdemli Hasta Danışmanı", "Hasta Koordinatörü", "Servis Sorumlusu", "Birim Yöneticisi", "Hasta Destek Personeli"];

const ORNEK_PERSONEL = [
  { id: 1, ad: "Ayşe", soyad: "Kaya", tcNo: "12345678901", dogumTarihi: "1990-05-15", telefon: "0532 111 2233", email: "ayse.kaya@hastane.com", cinsiyet: "Kadın", egitim: "Lisans - Sağlık Yönetimi", universite: "Hacettepe Üniversitesi", mezunYil: "2012", sertifikalar: "Hasta İletişimi Sertifikası, İlk Yardım", ilgiAlanlari: "Hasta psikolojisi, süreç iyileştirme", yetkinlikler: "İletişim, Empati, Problem Çözme", birim: "Hasta Hizmetleri", altBirim: "Poliklinik Karşılama", unvan: "Hasta Koordinatörü", konum: "Blok A - Zemin Kat", amiri: "Mehmet Yılmaz", iseBaslamaTarihi: "2015-03-01", foto: null, aktif: true, lokasyonTarihcesi: [{tarih: "2015-03-01", konum: "Blok B - 1. Kat", birim: "Acil Servis", unvan: "Hasta Destek Personeli"}, {tarih: "2018-06-15", konum: "Blok A - Zemin Kat", birim: "Hasta Hizmetleri", unvan: "Hasta Koordinatörü"}] },
  { id: 2, ad: "Mehmet", soyad: "Yılmaz", tcNo: "98765432109", dogumTarihi: "1985-11-20", telefon: "0533 444 5566", email: "mehmet.yilmaz@hastane.com", cinsiyet: "Erkek", egitim: "Yüksek Lisans - İşletme", universite: "ODTÜ", mezunYil: "2010", sertifikalar: "Liderlik, Kalite Yönetimi", ilgiAlanlari: "Yönetim, ekip geliştirme", yetkinlikler: "Liderlik, Organizasyon, Karar Verme", birim: "Hasta Hizmetleri", altBirim: "Yönetim", unvan: "Birim Yöneticisi", konum: "İdari Bina", amiri: "Dr. Fatma Demir", iseBaslamaTarihi: "2011-09-01", foto: null, aktif: true, lokasyonTarihcesi: [{tarih: "2011-09-01", konum: "Blok A - 1. Kat", birim: "Hasta Hizmetleri", unvan: "Hasta Hizmetleri Uzmanı"}, {tarih: "2016-01-01", konum: "İdari Bina", birim: "Hasta Hizmetleri", unvan: "Birim Yöneticisi"}] },
  { id: 3, ad: "Zeynep", soyad: "Arslan", tcNo: "55544433322", dogumTarihi: "1995-07-08", telefon: "0535 777 8899", email: "zeynep.arslan@hastane.com", cinsiyet: "Kadın", egitim: "Önlisans - Sağlık Hizmetleri", universite: "Ankara Meslek Yüksekokulu", mezunYil: "2015", sertifikalar: "Hasta İletişimi", ilgiAlanlari: "Pediatri, hasta takibi", yetkinlikler: "Sabır, İletişim, Organizasyon", birim: "Pediatri", altBirim: "Çocuk Polikliniği", unvan: "Hasta Hizmetleri Uzmanı", konum: "Blok B - 1. Kat", amiri: "Ayşe Kaya", iseBaslamaTarihi: "2017-05-15", foto: null, aktif: true, lokasyonTarihcesi: [{tarih: "2017-05-15", konum: "Blok B - 1. Kat", birim: "Pediatri", unvan: "Hasta Hizmetleri Uzmanı"}] },
];

const initialState = {
  personeller: ORNEK_PERSONEL,
