FROM ruby:3.4

# Instala dependências do sistema (ajuste se precisar)
RUN apt-get update -qq && apt-get install -y \
  build-essential \
  git \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copia arquivos de dependências primeiro (melhora cache)
COPY Gemfile Gemfile.lock ./

RUN bundle install

# Copia o restante do projeto
COPY . .

CMD ["bundle", "exec", "rspec"]