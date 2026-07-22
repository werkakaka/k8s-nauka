# Lekcja 008 – Probes (liveness, readiness, startup)

## Cel lekcji
Zrozumieć jak Kubernetes sprawdza czy aplikacja faktycznie działa poprawnie,
a nie tylko czy proces w kontenerze wciąż istnieje.

## Teoria
- STATUS: Running oznacza tylko, że proces w kontenerze się nie zakończył - nic nie mówi
  o tym, czy aplikacja faktycznie odpowiada poprawnie na żądania.
- livenessProbe - "czy aplikacja żyje?". Nieudana sonda -> Kubernetes zabija i restartuje kontener.
- readinessProbe - "czy aplikacja jest gotowa na ruch?". Nieudana sonda -> Pod znika z Endpoints
  w Service (nie dostaje ruchu), ale kontener NIE jest restartowany.
- startupProbe - dla wolno startujących aplikacji, wstrzymuje liveness/readiness dopóki
  startup się nie powiedzie.
- Domyślne wartości sondy: timeout=1s, #success=1 (ile kolejnych sukcesów by uznac za zdrowy),
  #failure=3 (ile kolejnych porażek by uznac za niezdrowy) - sonda nie reaguje na pojedyncze zająknięcie.
- Restart kontenera po jego zakończeniu (np. `nginx -s stop`) to podstawowy mechanizm kubelet +
  restartPolicy, NIEZALEŻNY od liveness probe. Liveness probe pokazuje swoją wartość dopiero gdy
  proces nadal działa, ale przestał odpowiadać poprawnie (zawieszenie bez zakończenia procesu) -
  bez sondy kubelet nie miałby o tym żadnego sygnału.
- CrashLoopBackOff - stan gdy kontener wielokrotnie i szybko się wywala, Kubernetes nakłada
  rosnące opóźnienia między restartami.

## Komendy
- `kubectl describe pod <nazwa>` - sekcje Liveness/Readiness pokazują konfigurację sond
- `kubectl get events --field-selector involvedObject.name=<nazwa>` - historia zdarzeń
  konkretnego obiektu
- `kubectl get pods -w` - podgląd statusu Podów na żywo (watch)

## Ćwiczenie praktyczne
Skonfigurowałam livenessProbe i readinessProbe (httpGet na port 80) dla Poda z nginx.
Zatrzymałam proces nginx wewnątrz kontenera (`nginx -s stop`) i zaobserwowałam automatyczny
restart kontenera przez kubelet (RESTARTS rosnące), przez chwilę widziałam też CrashLoopBackOff.

## Problemy i rozwiązania
- Test z `nginx -s stop` pokazał restart wynikający z zakończenia procesu (kubelet + restartPolicy),
  a nie stricte z liveness probe - zrozumiałam różnicę między tymi dwoma mechanizmami.

## Checklist
- [x] Rozumiem że Running != "aplikacja działa poprawnie"
- [x] Znam różnicę między liveness a readiness probe (restart vs usunięcie z ruchu)
- [x] Wiem po co jest startupProbe
- [x] Rozumiem różnicę między restartem z powodu zakończenia procesu a restartem z powodu liveness probe
- [x] Umiem skonfigurować probes w manifeście YAML
