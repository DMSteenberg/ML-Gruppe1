# filepath: /C:/Users/Daniel/Desktop/Skole/ML/ML-Gruppe1/project/Dockerfile
FROM ubuntu:latest

RUN apt-get update && apt-get install -y curl \
    && curl -fsSL https://ollama.com/install.sh | sh

WORKDIR /app


# Tilføjer en kopi af vores lokal model ind i docker Erstat med din egen path
COPY models/llama-2-7b.Q2_K.gguf ./llama-2-7b.Q2_K.gguf

# Variable
RUN echo 'FROM ./llama-2-7b.Q2_K.gguf' > Modelfile

# Mother script
# 1. Start Ollama
# 2. Sleep 5 sekunder
# 3. Opret model
# 4. Kør model
RUN echo '#!/bin/sh\n\
ollama start &\n\
sleep 5\n\
ollama create llama3.2 -f ./Modelfile && \n\
ollama run llama3.2' > /entrypoint.sh \
    && chmod +x /entrypoint.sh

EXPOSE 9000

CMD ["/entrypoint.sh"]
