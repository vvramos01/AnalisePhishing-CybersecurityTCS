#  Análise Técnica de E-mails de Phishing (Laboratório SOC)

Este repositório contém o desenvolvimento, roteiro e resultados do **Laboratório de Análise de Phishing**, focado na extração e investigação de artefactos técnicos a partir do código-fonte de amostras reais de e-mail no formato `.eml`.

---

##  Sobre o Projeto

O objetivo deste laboratório foi aplicar metodologias de análise de e-mails suspeitos utilizadas por analistas de SOC (Security Operations Center), realizando a extração de:
* **Cabeçalhos de autenticação:** SPF, DKIM e DMARC.
* **Caminho de rede:** IP e *hostname* do primeiro salto (*Received*).
* **URLs e Links:** Extração e desativação (*defang*) para análise segura.
* **Anexos:** Identificação de tipos de ficheiro e cálculo do *hash* SHA-256.
* **Técnicas de Engenharia Social:** Mapeamento de gatilhos psicológicos usados pelos atacantes.

As amostras foram obtidas a partir do repositório público **[phishing_pot](https://github.com/rf-peixoto/phishing_pot)** (mais de 12 mil e-mails reais capturados em *honeypots*).

---

##  Protocolos de Segurança Aplicados

* **Ambiente Isolado:** Toda a análise e manipulação dos ficheiros `.eml` foram realizadas exclusivamente no Google Colab.
* **Sem Download Local de Amostras Brutas:** Ficheiros maliciosos não foram descarregados para a máquina local.
* **Sanitização de URLs/IPs (*Defang*):** Aplicação de máscaras em domínios e IPs (ex.: `hxxp://site[.]com`) para evitar acessos acidentais.
* **Consultas Privadas:** Utilização do `urlscan.io` em modo *Private* e pesquisas prévias no *VirusTotal*.

---

##  Ficha de Entrega - Resultados da Análise

| Campo | Amostra 1 (nº 10) | Amostra 2 (nº 1000) | Amostra 3 (nº 10001) |
| :--- | :--- | :--- | :--- |
| **Assunto e Marca Imitada** | Microsoft account unusual signin activity (Microsoft) | Liberação de IRPF - 6NwLyfzWcsNerv0 / Receita Federal ou Banco do Brasil (`[BB]`) | 100 Balls. $5 No Deposit Required ! / Imitação de site de apostas (*free spin*) |
| **From** | `"Microsoft account team", _ <no-reply@access-accsecurity.com>` | `"[BB] - Seu saldo foi liberado - Código: 11084339647130851921" <prestonconstance587@gmail.com>` | `free spin <lee.white@bnvftbfantay.onmicrosoft.com>` |
| **Reply-To** | `sotrecognizd@gmail.com` | *None* | *None* |
| **Return-Path** | `bounce@thcultarfdes.co.uk` | `prestonconstance587@gmail.com` | `lee.white@bnvftbfantay.onmicrosoft.com` |
| **IP e Host do 1º Salto** | `thcultarfdes.co.uk (89.144.44.2)` | `a3.domain ([20.97.213.223]) by smtp.gmail.com` | `268422111889 named unknown by gmailapi.google.com` |
| **SPF / DKIM / DMARC** | `spf=none, dkim=none, dmarc=permerror` | `spf=pass, dkim=pass, dmarc=pass` | `spf=fail, dkim=pass, dmarc=none` |
| **URLs (com *defang*)** | `hxxp://thebandalisty[.]com/track/o43062rdzGz18708448Gdrw1821750fYo33632dSjh176` | *Nenhuma* | Várias iniciadas em `hxxp://woondsplay[.]com` e
