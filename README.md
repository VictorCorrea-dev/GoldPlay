## 7. Instruções para Executar os Testes ou Usar a Coleção de Requisições

### Execução de Testes Automatizados
Para executar a suíte de testes unitários e de contexto do Spring Boot via terminal:
```bash
./mvnw test
```

### Testes Manuais e Coleção de Requisições (Postman / Insomnia)
1. Com a API em execução em `http://localhost:8080`, abra o **Postman**, **Insomnia** ou o próprio **Front-end (`index.html`)**.
2. Cadastre primeiro os registros base (`POST /pacientes`, `POST /dentistas`, `POST /procedimentos` e `POST /consultorios`).
3. Para testar a criação de um agendamento (`POST http://localhost:8080/agendamentos`), utilize o seguinte exemplo de corpo JSON (`Content-Type: application/json`):
   ```json
   {
     "dataHora": "2026-12-10T14:30:00",
     "observacoes": "Avaliação inicial",
     "paciente": { "id": 1 },
     "dentista": { "id": 1 },
     "procedimento": { "id": 1 },
     "consultorio": { "id": 1 }
   }
   ```
4. Para validar a regra de conflito de horário, tente enviar uma segunda requisição `POST /agendamentos` no mesmo horário para o mesmo `dentista` ou `consultorio` — a API retornará erro impedindo a sobreposição.

---
