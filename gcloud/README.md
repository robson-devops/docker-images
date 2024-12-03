# Google Cloud CLI

Criação de imagem Docker para a administração dos recursos computacionais GCP via linha de comando.  
Essa imagem poderá ser utilizada no Stage de Deploy de uma pipeline CI/CD.
A mesma precisará estar armazenada em um Registry público ou privado.

Fonte: https://cloud.google.com/cli?hl=pt-BR

## Pré-requisitos
Instalar as ferramentas Docker e Grype no máquina host.
- [Docker](https://docs.docker.com/desktop/) para a criação da imagem;
- [Grype](https://github.com/anchore/grype/) para o scanner da imagem.

## Construção da imagem

```bash
docker build --no-cache -t google-cloud-sdk:502.0.0 -f Dockerfile . 
```

## Verificação das vulnerabilidades de segurança

```bash
grype $(docker images | grep google-cloud-sdk | awk '{ print $3 }')
```

**Exemplo de saída do comando:**
```yaml
✔ Vulnerability DB                [no update available]
 ✔ Loaded image                                                                                                                 803e7d91d2b2
 ✔ Parsed image                                                      sha256:803e7d91d2b28af87e607da4fa160cda844e5e34ebaf8173f1d45a7f5b50b2e6
 ✔ Cataloged contents                                                       faa0ca9b2b8821b02066581ba89856d0e268606db0225754a556f394243f0f85
   ├── ✔ Packages                        [33 packages]
   ├── ✔ File digests                    [1,462 files]
   ├── ✔ File metadata                   [1,462 locations]
   └── ✔ Executables                     [110 executables]
 ✔ Scanned for vulnerabilities     [7 vulnerability matches]
   ├── by severity: 0 critical, 3 high, 3 medium, 0 low, 0 negligible (1 unknown)
   └── by status:   6 fixed, 1 not-fixed, 0 ignored
NAME        INSTALLED  FIXED-IN         TYPE       VULNERABILITY   SEVERITY
libcrypto3  3.3.2-r0   3.3.2-r1         apk        CVE-2024-9143   Medium
libssl3     3.3.2-r0   3.3.2-r1         apk        CVE-2024-9143   Medium
python3     3.12.7-r0                   apk        CVE-2024-9287   Unknown
stdlib      go1.22.4   1.22.7, 1.23.1   go-module  CVE-2024-34158  High
stdlib      go1.22.4   1.22.7, 1.23.1   go-module  CVE-2024-34156  High
stdlib      go1.22.4   1.21.12, 1.22.5  go-module  CVE-2024-24791  High
stdlib      go1.22.4   1.22.7, 1.23.1   go-module  CVE-2024-34155  Medium
```

## Execução do contêiner
```bash
docker run -it --name google-cloud-sdk $(docker images | grep google-cloud-sdk | awk '{ print $3 }') sh 
```

# Verificação da versão do gcloud 

```bash
gcloud version
```

<div align="center"><center><h6>:rocket: Go Devops... !!!</center></div>