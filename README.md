# LLM Benchmark (Ollama only)

This tool allows you to get the tokens per second (t/s) of Large Language Models (LLMs) running on your local machine. Currently, we only support testing Ollama models.

### Example output
Output on an Nvidia 4090 Windows desktop
```bash
Average stats:

----------------------------------------------------
        llama2:13b
                Prompt eval: 690.15 t/s
                Response: 78.27 t/s
                Total: 80.78 t/s

        Stats:
                Prompt tokens: 42
                Response tokens: 1155
                Model load time: 2.87s
                Prompt eval time: 0.06s
                Response time: 14.76s
                Total time: 17.69s
----------------------------------------------------

Average stats:

----------------------------------------------------
        llama2:latest
                Prompt eval: 1148.29 t/s
                Response: 123.31 t/s
                Total: 127.41 t/s

        Stats:
                Prompt tokens: 42
                Response tokens: 1122
                Model load time: 1.97s
                Prompt eval time: 0.04s
                Response time: 9.10s
                Total time: 11.11s
----------------------------------------------------
```

### Interactive Mode Preview
![Interactive Demo](interactive_demo.png)

## Getting Started

To set up and run benchmarks on your system, follow these instructions.

### Prerequisites

- Python 3.6+
- [Ollama](https://ollama.com/)

### Installation

1. **Clone this repository**

   Open a terminal or powershell and run:

   ```bash
   git clone https://github.com/willybcode/llm-benchmark.git
   cd llm-benchmark
   ```

2. **Create a virtual environment**

   - **Windows**

     ```bash
     python -m venv venv
     .\venv\Scripts\activate
     ```

   - **Linux/macOS**

     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Serve the Ollama models**

   Before running benchmarks, make sure your Ollama model server is running
   
   Try ```ollama list``` . If you get an error then run  ```ollama serve```


### Running Benchmarks
#### Interactive Mode
Run `benchmark.py` script with no arguments to start the interactive mode.

```bash
python benchmark.py
```

#### Command Line
Run the `benchmark.py` script with the desired command line arguments:

```bash
python benchmark.py --verbose --prompts "What is the sky blue?" "Write a report on the financials of Nvidia"
```

#### Command Line Arguments

- `-v` or `--verbose`: Prints the prompts and streams the responses from Ollama
- `-a` or `--all`: Use all available models.
- `-s` or `--skip-models`: To specify a list of model to skip during the benchmark. Separate multiple models with spaces.
- `-u` or `--use-models`: To specify a list of model to run during the benchmark. The benchmart will only run the specified models. Separate multiple models with spaces.
- `-p` or `--prompts`: Provide custom prompts to use for benchmarking. Separate multiple prompts with spaces.
- `--remote`: Use a remote ollama instance.

Note: Run `ollama list` in a terminal/command line to get names of the models available on your system. You can then use those names with the `-u` or `-s` arguments.

#### Examples

- **Run with default prompts in verbose mode**

  *Run a benchmark using the default prompts and print the output in verbose mode.*

  ```bash
  python benchmark.py --verbose --all
  ```

- **Run with custom prompts**

  *Skip one or more specific models during the benchmark. Run on all models except the ones specified.*

  ```bash
  python benchmark.py --all --prompts "Custom prompt 1" "Why is the sky blue?"
  ```

- **Skip specific models**

  *Skip one or more specific models during the benchmark. Run on all models except the ones specified.*

  ```bash
  python benchmark.py -s llama3.1:latest gemma2:9b # will run benchmark on all models except those two
  ```
- **Only use specific models**

  *Run a benchmark only on one or more specific models, even if other models are available.*

  ```bash
  python benchmark.py -u llama2:13b phi3:latest qwen2:72b # will run benchmark only on those three models if they are available
  ```

- **Run with remote host:port**

  *Run a benchmark using a remote Ollama instance.*

  ```bash
  python benchmark.py --remote http://localhost:11434
  ```

## Roadmap
### Upcoming Features
I am planning to add the following features to improve this project:

#### Current
- [x] Allow users to specify which models to run
- [x] Add support for an interactive mode
  - [x] Show numbered list of available models
  - [x] Add support for selecting models to skip or use
  - [x] Add support for verbose and prompts selection
- [x] Support using remote host:port
- [ ] Exclude the embedding models from benchmarking by default (they lack support for chat)
- [ ] Better error handling and documentation
- [ ] Add support for a configuration file

#### Future
- [ ] Retrieve and display hardware information
- [ ] Allow users to load a list of models from a file for `skip` or `use`
- [ ] Support saving well-formatted benchmark results to file
- [ ] Add support for colored output
- [ ] Explore options for optimizing resource usage


## Contributing

We appreciate your enthusiasm! Contributions are always welcome. To get started, you can submit a pull request or raise an issue if you have any suggestions for improvements or encounter bugs.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
