# Moja droga do Kubernetesa

Repozytorium dokumentujące naukę Kubernetesa. Każda lekcja ma swój folder z README, w którym opisuję co się nauczyłam, jakie komendy poznałam i jakie napotkałam problemy.

**Środowisko:** WSL2 (Ubuntu) + Docker + minikube + kubectl
**Cel:** praktyczna biegłość w K8s + certyfikat CKA


## Struktura repo

```
k8s-nauka/
├── README.md                      <- ten plik (roadmapa + postępy)
├── lekcje/
│   ├── 000-setup-srodowiska/
│   │   └── README.md
│   ├── 001-architektura-k8s/
│   │   └── README.md
│   ├── 002-pierwszy-pod/
│   │   └── README.md
│   └── ...
└── manifesty/                     <- pliki YAML z ćwiczeń
```

## Zasady prowadzenia repo

Każdy folder lekcji zawiera README z sekcjami:
- **Cel lekcji** – co mam umieć po jej zakończeniu
- **Teoria** – notatki własnymi słowami
- **Komendy** – lista poleceń z krótkim opisem co robią
- **Ćwiczenie praktyczne** – co zrobiłam w minikube
- **Problemy i rozwiązania** – na co się wywaliłam i jak to naprawiłam
- **Checklist** – zaznaczone punkty z tego, co potwierdzam że rozumiem

---

## Status nauki

Legenda: ⬜ nie zaczęte | 🟨 w trakcie | ✅ ukończone

### Moduł 0 – Przygotowanie środowiska
- ⬜ 000 – Instalacja: Docker, minikube, kubectl, konfiguracja WSL
- ⬜ 001 – Pierwsze uruchomienie klastra, `kubectl` podstawy, `kubeconfig`

### Moduł 1 – Fundamenty architektury
- ⬜ 002 – Architektura Kubernetesa (control plane vs worker nodes)
- ⬜ 003 – API Server, etcd, Scheduler, Controller Manager, kubelet, kube-proxy
- ⬜ 004 – Pody – czym są, cykl życia, multi-container pody
- ⬜ 005 – Namespace’y i organizacja zasobów
- ⬜ 006 – Labels, Selectors, Annotations

### Moduł 2 – Kontrolery i zarządzanie aplikacjami
- ⬜ 007 – ReplicaSet
- ⬜ 008 – Deployment – rolling update, rollback, strategie wdrożeń
- ⬜ 009 – DaemonSet
- ⬜ 010 – StatefulSet (i różnice względem Deployment)
- ⬜ 011 – Job i CronJob

### Moduł 3 – Sieć w Kubernetesie
- ⬜ 012 – Model sieciowy K8s (podstawy)
- ⬜ 013 – Service: ClusterIP, NodePort, LoadBalancer
- ⬜ 014 – DNS wewnątrz klastra (CoreDNS)
- ⬜ 015 – Ingress i Ingress Controller
- ⬜ 016 – NetworkPolicy – ograniczanie ruchu

### Moduł 4 – Konfiguracja i dane
- ⬜ 017 – ConfigMap
- ⬜ 018 – Secret
- ⬜ 019 – Volumes – emptyDir, hostPath
- ⬜ 020 – PersistentVolume i PersistentVolumeClaim
- ⬜ 021 – StorageClass i dynamiczne provisioning

### Moduł 5 – Bezpieczeństwo
- ⬜ 022 – ServiceAccount
- ⬜ 023 – RBAC – Role, RoleBinding, ClusterRole, ClusterRoleBinding
- ⬜ 024 – SecurityContext (użytkownik, capabilities, read-only fs)
- ⬜ 025 – Pod Security Standards / Admission

### Moduł 6 – Zasoby i skalowanie
- ⬜ 026 – Requests i Limits (CPU/RAM)
- ⬜ 027 – ResourceQuota i LimitRange
- ⬜ 028 – Probes: liveness, readiness, startup
- ⬜ 029 – Horizontal Pod Autoscaler (HPA)
- ⬜ 030 – Vertical Pod Autoscaler (VPA) – teoria

### Moduł 7 – Scheduling zaawansowany
- ⬜ 031 – nodeSelector i Node Affinity
- ⬜ 032 – Taints i Tolerations
- ⬜ 033 – Pod Affinity / Anti-Affinity
- ⬜ 034 – Topology Spread Constraints

### Moduł 8 – Zarządzanie pakietami
- ⬜ 035 – Helm – podstawy, chart, values.yaml
- ⬜ 036 – Tworzenie własnego Helm Charta
- ⬜ 037 – Kustomize (alternatywa dla Helm)

### Moduł 9 – Obserwowalność
- ⬜ 038 – Logi w K8s (`kubectl logs`, strategia logowania)
- ⬜ 039 – Metrics Server, `kubectl top`
- ⬜ 040 – Prometheus + Grafana w klastrze
- ⬜ 041 – Debugowanie: `describe`, `events`, `exec`, `port-forward`

### Moduł 10 – Troubleshooting
- ⬜ 042 – Typowe błędy: CrashLoopBackOff, ImagePullBackOff, Pending
- ⬜ 043 – Debugowanie sieci wewnątrz klastra
- ⬜ 044 – Debugowanie problemów ze storage

### Moduł 11 – Integracja z resztą stacku (masz już Docker + Terraform!)
- ⬜ 045 – Terraform + Kubernetes provider – zarządzanie zasobami K8s z Terraform
- ⬜ 046 – Podstawy GitOps – ArgoCD lub Flux
- ⬜ 047 – Prosty pipeline CI/CD budujący obraz Dockera i deployujący na K8s

### Moduł 12 – Klaster produkcyjny
- ⬜ 048 – kubeadm – budowa klastra od zera (multi-node, jeśli zasoby pozwolą)
- ⬜ 049 – Upgrade klastra
- ⬜ 050 – Backup i restore etcd, disaster recovery

### Moduł 13 – Przygotowanie do certyfikatu CKA
- ⬜ 051 – Format egzaminu CKA, zasady, zakres
- ⬜ 052 – Ćwiczenia z killer.sh / kodekloud (symulacje zadań)
- ⬜ 053 – Powtórka najsłabszych obszarów
- ⬜ 054 – Egzamin próbny na czas

---

## Zasoby, z których korzystam
- Dokumentacja oficjalna: https://kubernetes.io/docs/
- `kubectl` cheat sheet: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## 🛠️ Środowisko lokalne
```bash
minikube version
kubectl version --client
docker version
```
