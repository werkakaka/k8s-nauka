# Lekcja 003 – Services

## Cel lekcji
Zrozumieć jak udostępnić aplikację działającą w wielu Podach pod jednym, stałym adresem.

## Teoria
- Pody mają niestabilne adresy IP (zmieniają się przy self-healing) - potrzebny jest stały punkt dostępu.
- Service = stały adres/nazwa DNS, który kieruje ruch do Podów pasujących do etykiety (label selector),
  robiąc przy tym load balancing (round-robin) między nimi.
- Wewnętrzny DNS klastra (CoreDNS) pozwala łączyć się z Service po nazwie, nie tylko po IP.
- Typy Service:
  - ClusterIP (domyślny) - dostępny tylko wewnątrz klastra
  - NodePort - dodatkowo otwiera port na węźle, dostępny z zewnątrz
  - LoadBalancer - w chmurze tworzy zewnętrzny load balancer (w minikube: `minikube tunnel`)
- Domyślna restartPolicy Poda to Always - dlatego jednorazowe polecenia (jak `curl`) trzeba odpalać
  z `--restart=Never`, inaczej Kubernetes wpada w petle restartow (BackOff).

## Komendy
- `kubectl expose deployment <nazwa> --port=X --target-port=Y` - tworzy Service typu ClusterIP
- `kubectl expose deployment <nazwa> --port=X --target-port=Y --type=NodePort --name=<nazwa2>` - Service z dostępem z zewnątrz
- `kubectl get services` - lista Service'ów, ich typ, IP, porty
- `kubectl run <nazwa> --image=<obraz> --restart=Never -it --rm -- <komenda>` - tymczasowy Pod do testów jednorazowych
- `minikube service <nazwa> --url` - adres URL do Service NodePort w minikube (wymaga otwartego terminala na Linuksie/Docker driver)

## Ćwiczenie praktyczne
Stworzyłam Deployment (3 repliki nginx) + Service ClusterIP, sprawdziłam działanie
przez tymczasowego Poda z curl (DNS -> Service -> Pod zadziałało).
Dodałam drugi Service typu NodePort i zobaczyłam nginx bezpośrednio w przeglądarce.

## Problemy i rozwiązania
- Pod test-curl wpadł w BackOff, bo domyślna restartPolicy to Always, a curl to jednorazowe zadanie -
  naprawione przez `--restart=Never`.
- Klaster chwilowo nie odpowiadał (connection refused) - do sprawdzenia przez `minikube status`,
  naprawa: `minikube start`.

## Checklist
- [x] Rozumiem po co jest Service i jaki problem rozwiązuje
- [x] Rozumiem różnicę między ClusterIP, NodePort i LoadBalancer
- [x] Wiem jak Service znajduje swoje Pody (label selector)
- [x] Umiem stworzyć Service i przetestować go z poziomu klastra
- [x] Rozumiem różnicę między port-forward a Service
