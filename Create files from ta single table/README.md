---
title: "Criar pastas"
output: html_document
date: "2025-05-30"
---
```{r}

# Carregue os pacotes
library(readxl)
library(writexl)
library(fs)

# Caminho da pasta principal
pasta_principal <- "C:/Users/sampa/Documents/Doutorado/Dataset/Dothideomycetes_assembly/NCBI/Pleosporales_order_assemblies"

# Caminho do arquivo Excel
arquivo_excel <- file.path(pasta_principal, "Pleosporales_Order_with_Families.xlsx")

# Lê todos os nomes das planilhas
planilhas <- excel_sheets(arquivo_excel)

# Loop por cada planilha
for (nome_planilha in planilhas) {
  # Lê a planilha específica
  dados <- read_excel(arquivo_excel, sheet = nome_planilha)
  
  # Cria pasta específica para a família, se ainda não existir
  pasta_familia <- file.path(pasta_principal, nome_planilha)
  dir_create(pasta_familia)
  
  # Cria subpasta "All_assemblies" dentro da pasta da família
  subpasta_assemblies <- file.path(pasta_familia, "All_assemblies")
  dir_create(subpasta_assemblies)
  
  # Caminho para salvar o novo arquivo Excel
  caminho_saida <- file.path(pasta_familia, paste0(nome_planilha, ".xlsx"))
  
  # Salva a planilha individual dentro da pasta correspondente
  write_xlsx(dados, path = caminho_saida)
}

```

