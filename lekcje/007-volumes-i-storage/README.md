# Lekcja 007 – Volumes i przechowywanie danych

## Cel lekcji
Zrozumieć że kontenery są bezstanowe (dane znikają razem z kontenerem/Podem) i poznać
mechanizmy pozwalające danym przetrwać: emptyDir i PersistentVolumeClaim.

## Teoria
- Dane zapisane "w środku" kontenera znikają bezpowrotnie razem z nim (i Podem) - dokładnie
  jak w Dockerze.
- Volume = mechanizm podłączający zewnętrzne miejsce przechowywania danych do kontenera.
- `volumes` (poziom Poda) deklaruje CO istnieje, `volumeMounts` (poziom kontenera) deklaruje
  GDZIE to podłączyć w systemie plików kontenera. Rozdzielenie ma sens przy wielu kontenerach
  w jednym Podzie dzielących ten sam wolumen.
- emptyDir: pusty katalog tworzony przy starcie Poda. Przetrwa restart KONTENERA
  (bo Pod zostaje ten sam), ale znika przy usunięciu całego PODA.
- PersistentVolume (PV) = reprezentacja faktycznego kawałka pamięci masowej w klastrze.
- PersistentVolumeClaim (PVC) = "zamówienie" aplikacji na taki kawałek pamięci ("chcę 1Gi").
  Kubernetes dopasowuje/tworzy PV automatycznie (dynamic provisioning - w minikube dzięki
  dodatkowi storage-provisioner).
- PVC przetrwa usunięcie Poda - dane żyją niezależnie od cyklu życia konkretnego Poda,
  nowy Pod po prostu podłącza się do tego samego, istniejącego PVC.

## Komendy
- `kubectl exec -it <pod> -- sh -c "komenda"` - wykonanie komendy powłoki wewnątrz kontenera
- `kubectl apply -f <plik.yaml>` - tworzy PVC/Pod z manifestu
- `kubectl get pvc` - status PersistentVolumeClaim (Bound = poprawnie dopasowany do PV)
- `kubectl get pv` - lista PersistentVolume w klastrze

## Ćwiczenie praktyczne
Zapisałam plik w Podzie bez volume - po usunięciu i odtworzeniu Poda plik zniknął.
Zrobiłam to samo z emptyDir - plik przetrwał restart kontenera (nginx -s stop),
ale zniknął po usunięciu całego Poda.
Stworzyłam PVC (1Gi, ReadWriteOnce), podłączyłam go do Poda przez persistentVolumeClaim.claimName -
plik przetrwał NAWET usunięcie i odtworzenie całego Poda.

## Problemy i rozwiązania
(brak)

## Checklist
- [x] Rozumiem że kontenery/Pody są domyślnie bezstanowe
- [x] Znam różnicę między volumes (poziom Poda) a volumeMounts (poziom kontenera)
- [x] Rozumiem granice emptyDir (przetrwa restart kontenera, nie przetrwa usunięcia Poda)
- [x] Rozumiem relację PVC -> PV i dynamic provisioning
- [x] Widziałam na własne oczy że PVC przetrwa usunięcie Poda
