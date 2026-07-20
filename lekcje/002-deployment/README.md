# Lekcja 002 – Deployment

## Cel lekcji
Zrozumieć czym różni się Deployment od gołego Poda i zobaczyć mechanizm self-healing w akcji.

## Teoria
- Deployment = obiekt pilnujący, żeby zawsze istniała określona liczba kopii (replik) danego Poda.
- Kubernetes działa deklaratywnie: deklaruję STAN POŻĄDANY (np. "chcę 3 repliki"), a control loop w tle
  bez przerwy porównuje go ze STANEM AKTUALNYM i naprawia różnice.
- Deployment nie tworzy Podów bezpośrednio, tylko przez pośredni obiekt ReplicaSet.
- Self-healing: jeśli usunę/zabiję jeden Pod z Deploymentu, w kilka sekund powstaje nowy w jego miejsce.
- Skalowanie: zmiana liczby replik w locie, bez przestoju - Kubernetes dodaje/usuwa tylko różnicę.
- Usunięcie Deploymentu usuwa też wszystkie jego Pody (w przeciwieństwie do usuwania pojedynczego Poda).

## Komendy
- `kubectl create deployment <nazwa> --image=<obraz> --replicas=N` - tworzy Deployment z N replikami
- `kubectl get deployments` - status Deploymentu (READY, UP-TO-DATE, AVAILABLE)
- `kubectl scale deployment <nazwa> --replicas=N` - zmiana liczby replik w locie
- `kubectl rollout status deployment <nazwa>` - sprawdzenie czy rollout się ustabilizował
- `kubectl delete deployment <nazwa>` - usuwa Deployment i wszystkie jego Pody

## Ćwiczenie praktyczne
Stworzyłam Deployment z 3 replikami nginx, ręcznie usunęłam jeden Pod i zaobserwowałam,
że w ~13 sekund Kubernetes stworzył nowy w jego miejsce (self-healing).
Przeskalowałam Deployment do 5 replik na żywo, sprawdziłam rollout status.

## Problemy i rozwiązania
(brak)

## Checklist
- [x] Rozumiem różnicę między gołym Podem a Deploymentem
- [x] Rozumiem koncepcję stanu pożądanego vs aktualnego (control loop)
- [x] Widziałam self-healing na żywo
- [x] Umiem skalować Deployment
