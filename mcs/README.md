
Определяем настройки в файле: config



kubectl config --kubeconfig=config set-cluster mcs.slurm.io --server=https://5.188.142.58:6443 --certificate-authority=fake-ca-file
kubectl config --kubeconfig=config set-cluster scratch --server=https://5.6.7.8 --insecure-skip-tls-verify

