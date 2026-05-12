# Sistema de Câmera com IA (RTSP + Processamento em Servidor)

## Visão Geral

Este projeto consiste em um sistema de captura e processamento de vídeo utilizando Inteligência Artificial.

O fluxo principal é:

1. Captura de vídeo via RTSP
2. Envio/consumo do stream pelo servidor
3. Processamento com IA
4. Retorno da resposta (detecção, classificação, etc.)

---

## Arquitetura

```
[Câmera IP]
     │ (RTSP)
     ▼
[Servidor de Processamento]
     │
     ├── Captura de frames
     ├── Processamento com IA
     └── Retorno de resultados
[Cliente]
     │
     └── Consome resultado via VLC
```

---

## Captura de Vídeo (RTSP)

A câmera IP disponibiliza o stream de vídeo através do protocolo **RTSP (Real Time Streaming Protocol)**.

Exemplo de URL da câmera:

```
rtsp://admin:Abc.12345@192.168.1.64/ch0/stream0

rtsp://admin:Abc.12345@192.168.1.64/ch1/stream0
```

O servidor consome esse canal 0 continuamente para extrair frames. O ideal será combinar os dois canais para realizar a identificação de fumaça com maior acurácia.

---

## Processamento no Servidor

O servidor é responsável por:

* Conectar ao stream RTSP
* Aplicar modelo de Inteligência Artificial (Primeiramente se utilizou modelos prontos YOLO)
* Gerar stream de saída (Isso está momentâneo pelo menos)

### Pipeline de processamento
Toda essa pipeline foi a princípio feita em um script python:

1. Captura do frame
2. Pré-processamento (resize, normalização, etc.)
3. Inferência com modelo de IA
4. Pós-processamento (ex: bounding boxes, labels)
---

## Tecnologias Utilizadas

* RTSP (streaming de vídeo)
* Python / OpenCV (captura e processamento)
* Biblioteca de IA (YOLOv8)
---
