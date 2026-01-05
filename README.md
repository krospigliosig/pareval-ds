# Evaluación de DeepSeek con ParEval

Este repositorio es una edición de [ParEval](https://github.com/parallelcodefoundry/ParEval) que evalúa la habilidad de ```deepseek-coder-6.7b-base``` para generar código paralelo.

## Parámetros de evaluación

La evaluación se realizó bajo los siguientes parámetros:

- Temperatura: 0.2
- Top p: 0.95
- Tamaño del batch: 1
- Número máximo de tokens: 256
- Número de samples por prompt: 8
- Sampleo: activado

## Pipeline de ejecución

La ejecución se llevó a cabo a través de la siguiente secuencia de pasos:

- Generación de respuestas de ```deepseek-coder-6.7b-base``` con base en los problemas establecidos en el paper original
Comando: ```python generate.py --prompts ../prompts/generation-prompts-first-half.json --model deepseek-ai/deepseek-coder-6.7b-base --output resultados.json --cache cache.jsonl --max_new_tokens 256 --do_sample --batch_size 1 --num_samples_per_prompt 8```
- Compilación de respuestas generadas con ```deepseek-coder-6.7b-base``` a los problemas propuestos
Comando: ```python ./run-all.py ../generate/resultados.json -o resultados_ejecutados.json --exclude-models hip```
- Generación del dataframe de resultados de la salida de ```deepseek-coder-6.7b-base```
Comando: ```python ./create-dataframe.py ../drivers/resultados_ejecutados.json -o resultados.csv```
- Extracción de métricas de evaluación para la salida de ```deepseek-coder-6.7b-base``` a partir del dataframe
Comando: ```python ./metrics.py resultados.csv -o resultados_metrics.csv```

## Artículo original: Can Large Language Models Write Parallel Code?

Nichols, D., Davis, J. H., Xie, Z., Rajaram, A., & Bhatele, A. (2024, June). Can large language models write parallel code?. In *Proceedings of the 33rd International Symposium on High-Performance Parallel and Distributed Computing* (pp. 281-294).

### Citación (bibtex):

```
@misc{nichols2024large,
      title={Can Large Language Models Write Parallel Code?}, 
      author={Daniel Nichols and Joshua H. Davis and Zhaojun Xie and 
              Arjun Rajaram and Abhinav Bhatele},
      year={2024},
      publisher = {Association for Computing Machinery},
      address = {New York, NY, USA},
      booktitle = {Proceedings of the 33rd International Symposium on High-Performance Parallel and Distributed Computing},
      series = {HPDC '24}
}
```

## License

ParEval is distributed under the terms of the [MIT license](/LICENSE).
