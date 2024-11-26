# MeasureSleep

*Measure Sleep* é um método usado para medir o tempo de execução ou atraso entre comandos em um sistema, especialmente para testar a precisão de processos que dependem de intervalos específicos.
Ele funciona ao calcular o tempo real que o sistema "dorme" (pausa) em comparação com o tempo esperado, ajudando a identificar desvios ou inconsistências. É muito utilizado em cenários onde frações de milissegundos podem impactar o desempenho, como jogos, automação e análise de input lag.

Em resumo, o Measure Sleep é uma ferramenta prática para verificar se o sistema está cumprindo os tempos de espera programados corretamente.

## Codigo simples
caso tenha interesse em criar o seu propio measure spleep, abaixo está um codigo simples em python que faz essa respectiva função

```

import time

def measure_sleep(sleep_duration, iterations=10):
    deviations = []
    print(f"Medindo a precisão para um sleep de {sleep_duration} segundos ({iterations} iterações)...\n")
    
    for i in range(iterations):
        start_time = time.perf_counter()  
        time.sleep(sleep_duration)      
        end_time = time.perf_counter()   
        
        actual_sleep = end_time - start_time
        deviation = actual_sleep - sleep_duration
        deviations.append(deviation)
        
        print(f"Iteração {i+1}: Esperado = {sleep_duration:.6f}s, Real = {actual_sleep:.6f}s, Desvio = {deviation:.6f}s")
    
    avg_deviation = sum(deviations) / len(deviations)
    print(f"\nMédia de Desvio: {avg_deviation:.6f}s")
    return deviations

sleep_time = 0.01  
iterations = 20

# Executa o teste
measure_sleep(sleep_time, iterations)

```

## Explicação do código:

**time.perf_counter():** Utiliza um contador de alta precisão para medir o tempo real antes e depois do time.sleep.

**time.sleep(sleep_duration):** Faz uma pausa pelo tempo esperado.

**Desvio calculado:** O código subtrai o tempo esperado (sleep_duration) do tempo real para determinar o desvio.

**Iterações:** Mede várias vezes para obter uma média dos desvios.
