# Lekcja 001 – Pierwszy Pod

## Cel lekcji
Uruchomić pierwszy Pod w Kubernetesie, zrozumieć jego cykl życia i podstawowe komendy do jego inspekcji.

## Teoria
- Pod = najmniejsza jednostka w K8s, "opakowanie" na 1+ kontenerów działających razem na tym samym węźle.
- W K8s nigdy nie uruchamia się kontenerów bezpośrednio - zawsze przez Poda.
- Pod jest efemeryczny - jeśli go usuniesz albo umrze, nie wraca sam z siebie (to zadanie dla Deploymentów - następna lekcja).
- Stany Poda: Pending -> Running -> Succeeded/Failed (albo CrashLoopBackOff jeśli kontener ciągle pada).

## Komendy
- `kubectl run <nazwa> --image=<obraz>` - tworzy pojedynczy Pod
- `kubectl get pods` - lista Podów i ich statusu
- `kubectl describe pod <nazwa>` - pełne szczegóły + Events (log zdarzeń, przydatne do debugowania)
- `kubectl logs <nazwa>` - logi aplikacji wewnątrz kontenera
- `kubectl port-forward pod/<nazwa> <lokalny-port>:<port-w-podzie>` - tunel do Poda z mojego komputera
- `kubectl delete pod <nazwa>` - usuwa Poda (i nie wraca sam!)

## Ćwiczenie praktyczne
Uruchomiłam Poda z obrazem nginx, sprawdziłam status (Running, 1/1),
przejrzałam Events w describe (Pulled, Created, Started),
zrobiłam port-forward na 8080 i zobaczyłam stronę powitalną nginx w przeglądarce,
usunęłam Poda i potwierdziłam że sam nie wraca.

## Problemy i rozwiązania
(brak)

## Checklist
- [x] Rozumiem czym jest Pod i czym różni się od kontenera Dockera
- [x] Umiem stworzyć Poda przez kubectl run
- [x] Umiem sprawdzić status i logi Poda
- [x] Umiem zrobić port-forward do Poda
- [x] Wiem, że goły Pod nie odtwarza się sam po usunięciu
