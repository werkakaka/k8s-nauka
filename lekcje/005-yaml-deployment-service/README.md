# Lekcja 005 – Deployment + Service w pełnym YAML

## Cel lekcji
Napisać kompletny manifest łączący Deployment i Service, zrozumieć strukturę YAML
i przejść w pełni na podejście deklaratywne.

## Teoria
- apiVersion różni się w zależności od typu obiektu (Pod/Service/ConfigMap/Secret = v1,
  Deployment/ReplicaSet/StatefulSet = apps/v1). Nie trzeba się tego uczyć na pamięć -
  `kubectl api-resources` i `kubectl explain <obiekt>` to sprawdzają.
- `spec.selector.matchLabels` w Deployment i `template.metadata.labels` MUSZĄ się zgadzać -
  to jak Deployment wie, którymi Podami zarządza.
- `spec.selector` w Service musi pasować do labels na Podach - to "most" łączący Service z Podami,
  niezależny od Deploymentu.
- `---` w YAML pozwala umieścić kilka obiektów w jednym pliku.
- `kubectl apply -f` jest w pełni deklaratywne: edytuję plik, apply nalicza różnicę i naprawia tylko to,
  co się zmieniło (np. zmiana replicas 3->4 dodała tylko 1 nowy Pod, reszta się nie ruszyła).
- `kubectl delete -f <plik>` usuwa wszystkie obiekty z manifestu jedną komendą.

## Komendy
- `kubectl api-resources` - lista wszystkich typów obiektów z ich apiVersion
- `kubectl api-resources | grep -i <nazwa>` - filtrowanie listy
- `kubectl explain <obiekt>` - dokumentacja struktury danego obiektu wprost w terminalu
- `kubectl explain <obiekt>.spec.pole` - zejście głębiej w strukturę
- `kubectl apply -f <plik.yaml>` - tworzy lub aktualizuje obiekty z manifestu
- `kubectl delete -f <plik.yaml>` - usuwa wszystkie obiekty z manifestu
- `kubectl get deployments,pods,services` - kilka typów zasobów w jednej komendzie
- `kubectl get all` - większość podstawowych obiektów w namespace naraz
- `kubectl describe service <nazwa>` - sprawdzenie pola Endpoints (czy Service widzi Pody)

## Ćwiczenie praktyczne
Napisałam manifest z Deployment (3 repliki nginx) + Service (ClusterIP) w jednym pliku.
Sprawdziłam Endpoints w Service - 3 adresy IP:port, po jednym na Poda.
Zmieniłam replicas na 4 w pliku, zrobiłam apply - Kubernetes dodał tylko 1 nowy Pod.
Usunęłam wszystko jedną komendą `kubectl delete -f`.

## Problemy i rozwiązania
- Nie wiedziałam skąd brać apiVersion dla różnych obiektów - odkryłam `kubectl api-resources`
  i `kubectl explain` jako wbudowaną dokumentację.

## Checklist
- [x] Umiem napisać manifest z kilkoma obiektami w jednym pliku (Deployment + Service)
- [x] Rozumiem powiązanie selector/labels między Deployment a Podami, i Service a Podami
- [x] Wiem jak sprawdzić apiVersion i strukturę dowolnego obiektu (api-resources, explain)
- [x] Rozumiem że apply jest deklaratywne i nalicza tylko różnicę
- [x] Umiem usunąć wszystkie obiekty z manifestu jedną komendą
