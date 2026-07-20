# Lekcja 000 – Przygotowanie środowiska

## Cel lekcji
Zainstalować minikube i uruchomić pierwszy lokalny klaster Kubernetesa w WSL.

## Teoria
- Docker = narzędzie do uruchamiania pojedynczych kontenerów.
- Kubernetes = system zarządzający wieloma kontenerami na wielu serwerach (automatyczny restart, skalowanie, rozkładanie obciążenia).
- Klaster = grupa serwerów (nodes) zarządzanych razem. Dzieli się na control plane (mózg - podejmuje decyzje) i worker nodes (mięśnie - uruchamiają kontenery/Pody).
- minikube = narzędzie symulujące cały klaster (control plane + worker) w jednym kontenerze Docker, na potrzeby nauki.

## Komendy
- `curl -LO ...` – pobranie binarki minikube
- `sudo install ... /usr/local/bin/minikube` – instalacja minikube jako komendy systemowej
- `minikube start --driver=docker` – uruchomienie klastra K8s wewnątrz kontenera Docker
- `kubectl get nodes` – lista węzłów w klastrze, sprawdzenie czy są w stanie Ready

## Ćwiczenie praktyczne
Zainstalowałam minikube v1.38.1, uruchomiłam klaster (Kubernetes v1.35.1),
zweryfikowałam działanie przez `kubectl get nodes` - węzeł "minikube" w stanie Ready.

## Problemy i rozwiązania
(brak / opisz jeśli coś Ci się wywaliło)

## Checklist
- [x] Rozumiem różnicę między Dockerem a Kubernetesem
- [x] Wiem czym jest control plane, a czym worker node
- [x] Umiem uruchomić klaster minikube
- [x] Umiem sprawdzić status węzłów przez kubectl
