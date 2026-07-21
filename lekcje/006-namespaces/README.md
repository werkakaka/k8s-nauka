# Lekcja 006 – Namespace'y

## Cel lekcji
Zrozumieć po co dzieli się klaster na namespace'y i zobaczyć jak wewnętrznie
zbudowany jest sam Kubernetes (kube-system).

## Teoria
- Namespace = logiczny, izolowany "folder" w klastrze. Obiekty w różnych namespace'ach
  mogą mieć tę samą nazwę bez konfliktu.
- Kubernetes tworzy sam kilka namespace'ów: default (tu ląduje wszystko bez podanego -n),
  kube-system (wewnętrzne komponenty klastra), kube-public, kube-node-lease.
- Komponenty control plane (etcd, api-server, scheduler, controller-manager) i CoreDNS/kube-proxy
  to zwykłe Pody działające w namespace kube-system - nie ma w tym magii.
- Można zmienić domyślny namespace dla kubectl przez `kubectl config set-context --current --namespace=X`,
  żeby nie dopisywać -n do każdej komendy.
- `kubectl delete namespace X` usuwa CAŁY namespace razem ze wszystkim, co w nim jest - trzeba uważać.

## Komendy
- `kubectl get namespaces` - lista namespace'ów w klastrze
- `kubectl get pods -n <namespace>` - Pody w konkretnym namespace
- `kubectl create namespace <nazwa>` - tworzy nowy namespace
- `kubectl run <nazwa> --image=<obraz> -n <namespace>` - tworzy Poda w konkretnym namespace
- `kubectl config set-context --current --namespace=<nazwa>` - zmienia domyślny namespace dla kubectl
- `kubectl delete namespace <nazwa>` - usuwa cały namespace ze wszystkim w środku

## Ćwiczenie praktyczne
Zajrzałam do namespace kube-system i zobaczyłam tam wszystkie komponenty control plane jako
zwykłe Pody (etcd, kube-apiserver, kube-scheduler, kube-controller-manager, coredns, kube-proxy).
Stworzyłam własny namespace "moj-projekt", umieściłam w nim Poda i potwierdziłam, że jest
niewidoczny w namespace default (izolacja). Zmieniłam i przywróciłam domyślny namespace.

## Problemy i rozwiązania
(brak)

## Checklist
- [x] Rozumiem po co są namespace'y i jaki problem rozwiązują
- [x] Wiem jakie namespace'y Kubernetes tworzy sam i do czego służą
- [x] Umiem tworzyć obiekty w konkretnym namespace i przełączać się między nimi
- [x] Widziałam, że komponenty control plane to zwykłe Pody w kube-system
