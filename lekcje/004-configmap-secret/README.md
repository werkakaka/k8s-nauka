# Lekcja 004 – ConfigMap i Secret

## Cel lekcji
Nauczyć się oddzielać konfigurację od kodu aplikacji i bezpiecznie (na tyle na ile Secret to umożliwia)
przekazywać dane wrażliwe do Podów.

## Teoria
- ConfigMap = obiekt na jawne dane konfiguracyjne (adresy, nazwy, flagi), niezależne od obrazu kontenera.
- Secret = jak ConfigMap, ale do danych wrażliwych (hasła, tokeny). Dane zakodowane w Base64.
- WAŻNE: Base64 to NIE jest szyfrowanie - to tylko kodowanie, łatwo odwracalne. Secret sam w sobie
  nie jest w pełni bezpieczny - potrzebne dodatkowe mechanizmy (RBAC, szyfrowanie etcd, Vault) - temat na później.
- kubectl describe secret celowo nie pokazuje wartości (tylko liczbę bajtów) jako pierwsza warstwa ochrony.
- Przejście z podejścia imperatywnego (`kubectl run`, `kubectl create`) na deklaratywne (pliki YAML +
  `kubectl apply -f`) - standard pracy w prawdziwych projektach, bo niektórych rzeczy (jak podłączenie
  ConfigMap) nie da się zrobić samymi flagami w kubectl run.

## Komendy
- `kubectl create configmap <nazwa> --from-literal=KLUCZ=WARTOSC` - tworzy ConfigMap
- `kubectl create secret generic <nazwa> --from-literal=KLUCZ=WARTOSC` - tworzy Secret
- `kubectl apply -f <plik.yaml>` - tworzy/aktualizuje obiekt na podstawie manifestu YAML (deklaratywnie)
- `kubectl exec <pod> -- <komenda>` - wykonuje komendę wewnątrz działającego kontenera
- `kubectl get secret <nazwa> -o jsonpath='{.data.KLUCZ}' | base64 --decode` - odczyt prawdziwej wartości Secretu

## Ćwiczenie praktyczne
Stworzyłam ConfigMap i Secret z linii komend. Napisałam pierwszy manifest YAML (Pod z envFrom
wskazującym na ConfigMap), zastosowałam go przez `kubectl apply -f`. Sprawdziłam przez `kubectl exec ... env`,
że zmienne środowiskowe z ConfigMap trafiły do kontenera. Zdekodowałam wartość z Secretu z Base64.

## Problemy i rozwiązania
- `kubectl run` nie ma flagi `--env-from` - trzeba było przejść na manifest YAML i `kubectl apply -f`,
  co i tak jest właściwym, docelowym sposobem pracy z Kubernetesem.

## Checklist
- [x] Rozumiem po co oddzielać konfigurację od kodu/obrazu
- [x] Znam różnicę między ConfigMap a Secret
- [x] Wiem, że Base64 to nie jest szyfrowanie
- [x] Umiem napisać prosty manifest YAML dla Poda
- [x] Umiem podłączyć ConfigMap jako zmienne środowiskowe przez envFrom
- [x] Umiem odczytać wartość z Secretu
