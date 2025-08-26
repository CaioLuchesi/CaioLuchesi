## 
<div align="center">
  <a href="https://github.com/CaioLuchesi">
  <img height="160em" src="https://github-readme-stats.vercel.app/api?username=CaioLuchesi&show_icons=true&theme=monokai&include_all_commits=true&count_private=true"/>
  <img height="160em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=CaioLuchesi&layout=compact&langs_count=10&theme=monokai"/>
</div>
<div style="display: inline-block"><br>
  <img align="center" alt="CaioLuchesi-NET" src="https://img.shields.io/badge/.NET-5C2D91?style=for-the-badge&logo=.net&logoColor=white">
  <img align="center" alt="CaioLuchesi-Csharp" src="https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white">
  <img align="center" alt="CaioLuchesi-C" src="https://img.shields.io/badge/C-00599C?style=for-the-badge&logo=c&logoColor=white">
  <img align="center" alt="CaioLuchesi-C++" src="https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=c%2B%2B&logoColor=white">
  <img align="center" alt="CaioLuchesi-Java" src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white">
  <img align="center" alt="CaioLuchesi-PHP" src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white">
  <img align="center" alt="CaioLuchesi-Python" src="https://img.shields.io/badge/Python-14354C?style=for-the-badge&logo=python&logoColor=white">
  <img align="center" alt="CaioLuchesi-Js" src="https://img.shields.io/badge/JavaScript-323330?style=for-the-badge&logo=javascript&logoColor=F7DF1Ek">
  <img align="center" alt="CaioLuchesi-Ts"  src="https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white">
  <img align="center" alt="CaioLuchesi-React"  src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
  <img align="center" alt="CaioLuchesi-ReactNative" = src="https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB">
  <img align="center" alt="CaioLuchesi-Angular" src="https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white">
  <img align="center" alt="CaioLuchesi-AngularJS" src="https://img.shields.io/badge/AngularJS-E23237?style=for-the-badge&logo=angularjs&logoColor=white">
  <img align="center" alt="CaioLuchesi-Node" src="https://img.shields.io/badge/Node.js-43853D?style=for-the-badge&logo=node.js&logoColor=white">
  <img align="center" alt="CaioLuchesi-HTML"  src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
  <img align="center" alt="CaioLuchesi-CSS"  src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white">
  <img align="center" alt="CaioLuchesi-Sass" src="https://img.shields.io/badge/Sass-CC6699?style=for-the-badge&logo=sass&logoColor=white">
  <img align="center" alt="CaioLuchesi-Bootstrap" src="https://img.shields.io/badge/Bootstrap-563D7C?style=for-the-badge&logo=bootstrap&logoColor=white">
  <img align="center" alt="CaioLuchesi-styledcomponents" src="https://img.shields.io/badge/styled--components-DB7093?style=for-the-badge&logo=styled-components&logoColor=white">
  <img align="center" alt="CaioLuchesi-MongoDB" src="https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white">
  <img align="center" alt="CaioLuchesi-Microsoft_SQL_Server" src="https://img.shields.io/badge/Microsoft_SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white">
  <img align="center" alt="CaioLuchesi-Microsoft_Azure" src="https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white">
</div>
  
  ##
 
<div> 
  <a href="https://www.linkedin.com/in/caio-fernandes-luchesi" target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white"></a> 
  <a href = "mailto:caiofluchesi@gmail.com"  target="_blank" rel="noopener noreferrer"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white"></a>
  
  ![Snake animation](https://github.com/CaioLuchesi/CaioLuchesi/blob/main/grid-snake.svg)
<!--   [![Readme Card](https://github-readme-stats.vercel.app/api/pin/?username=CaioLuchesi&repo=BomberBro)](https://github.com/CaioLuchesi/BomberBro) -->
</div>

param(
  [string]$DnsName   = "example.local",
  [string]$OutDir    = "$env:USERPROFILE\cert-out",
  [string]$PfxPass   = "ChangeMe#2025"     # pode trocar ou passar por parâmetro
)

# ---- Pré-checagens -----------------------------------------------------------
if (-not (Get-Command openssl -ErrorAction SilentlyContinue)) {
  throw "OpenSSL não encontrado no PATH. Instale-o ou adicione ao PATH e tente novamente."
}
New-Item -ItemType Directory -Path $OutDir -Force | Out-Null

# ---- 1) Certificado autoassinado --------------------------------------------
$secure = ConvertTo-SecureString -String $PfxPass -AsPlainText -Force
$cert = New-SelfSignedCertificate `
  -DnsName $DnsName `
  -CertStoreLocation Cert:\CurrentUser\My `
  -KeyExportPolicy Exportable `
  -KeyAlgorithm RSA -KeyLength 4096 `
  -HashAlgorithm SHA256 `
  -NotAfter (Get-Date).AddYears(2) `
  -FriendlyName "SelfSigned $DnsName"

# ---- 2) Exporta PFX e CER (DER) ---------------------------------------------
$pfxPath = Join-Path $OutDir "$($DnsName).pfx"
$cerDer  = Join-Path $OutDir "$($DnsName).cer"    # DER (binário)
Export-PfxCertificate -Cert $cert -FilePath $pfxPath -Password $secure | Out-Null
Export-Certificate   -Cert $cert -FilePath $cerDer -Type CERT        | Out-Null

# ---- 3) Extrai CERT e KEY em PEM via OpenSSL -------------------------------
$certPem = Join-Path $OutDir "$($DnsName).crt.pem" # apenas o certificado (PEM)
$keyPem  = Join-Path $OutDir "$($DnsName).key.pem" # chave privada (PEM, sem senha)
$fullPem = Join-Path $OutDir "$($DnsName).fullchain.pem" # self-signed == igual ao cert

# certificado (sem chave)
cmd /c "openssl pkcs12 -in `"$pfxPath`" -clcerts -nokeys -passin pass:$PfxPass -out `"$certPem`""
# chave privada (sem senha)
cmd /c "openssl pkcs12 -in `"$pfxPath`" -nocerts -nodes  -passin pass:$PfxPass -out `"$keyPem`""

Copy-Item $certPem $fullPem -Force   # em CA própria/self-signed o fullchain = cert

# ---- 4) Função utilitária para Base64 ---------------------------------------
function Write-Base64File([string]$inputPath, [string]$outputPath) {
  $bytes  = [System.IO.File]::ReadAllBytes($inputPath)
  $b64    = [System.Convert]::ToBase64String($bytes)
  Set-Content -Path $outputPath -Value $b64 -NoNewline -Encoding ASCII
}

# ---- 5) Gera arquivos em Base64 (um .b64.txt para cada artefato) -----------
$pfxB64 = Join-Path $OutDir "$($DnsName).pfx.b64.txt"
$cerB64 = Join-Path $OutDir "$($DnsName).cer.der.b64.txt"
$crtPemB64 = Join-Path $OutDir "$($DnsName).crt.pem.b64.txt"
$keyPemB64 = Join-Path $OutDir "$($DnsName).key.pem.b64.txt"
$fullPemB64= Join-Path $OutDir "$($DnsName).fullchain.pem.b64.txt"

Write-Base64File $pfxPath  $pfxB64
Write-Base64File $cerDer   $cerB64
Write-Base64File $certPem  $crtPemB64
Write-Base64File $keyPem   $keyPemB64
Write-Base64File $fullPem  $fullPemB64

# ---- 6) JSON consolidado com todos os Base64 (útil para colar em secrets) ---
$jsonOut = Join-Path $OutDir "$($DnsName).all_base64.json"
$payload = [ordered]@{
  dnsName             = $DnsName
  pfx_base64          = Get-Content $pfxB64  -Raw
  cer_der_base64      = Get-Content $cerB64  -Raw
  cert_pem_base64     = Get-Content $crtPemB64 -Raw
  key_pem_base64      = Get-Content $keyPemB64 -Raw
  fullchain_pem_base64= Get-Content $fullPemB64 -Raw
}
$payload | ConvertTo-Json -Depth 5 | Set-Content -Path $jsonOut -Encoding UTF8

# ---- 7) Resumo --------------------------------------------------------------
@"
✅ Gerado em: $OutDir

Arquivos binários/texto:
- $pfxPath
- $cerDer
- $certPem
- $keyPem
- $fullPem

Arquivos Base64 (conteúdo sem quebras de linha):
- $pfxB64
- $cerB64
- $crtPemB64
- $keyPemB64
- $fullPemB64

JSON consolidado:
- $jsonOut
"@ | Write-Host
