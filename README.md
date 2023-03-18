## `tiktoken-rs`

[![Github Contributors](https://img.shields.io/github/contributors/zurawiki/tiktoken-rs.svg)](https://github.com/zurawiki/tiktoken-rs/graphs/contributors)
[![Github Stars](https://img.shields.io/github/stars/zurawiki/tiktoken-rs.svg)](https://github.com/zurawiki/tiktoken-rs/stargazers)
[![CI](https://github.com/zurawiki/tiktoken-rs/actions/workflows/ci.yml/badge.svg)](https://github.com/zurawiki/tiktoken-rs/actions/workflows/ci.yml)

[![crates.io status](https://img.shields.io/crates/v/tiktoken-rs.svg)](https://crates.io/crates/tiktoken-rs)
[![crates.io downloads](https://img.shields.io/crates/d/tiktoken-rs.svg)](https://crates.io/crates/tiktoken-rs)
[![Rust dependency status](https://deps.rs/repo/github/zurawiki/tiktoken-rs/status.svg)](https://deps.rs/repo/github/zurawiki/tiktoken-rs)

Rust library for tokenizing text with OpenAI models using tiktoken.

This library provides a set of ready-made tokenizer libraries for working with GPT, tiktoken and related OpenAI models. Use cases covers tokenizing and counting tokens in text inputs.

This library is built on top of the `tiktoken` library and includes some additional features and enhancements for ease of use with rust code.

# Examples

For full working examples for all supported features, see the [examples](https://github.com/zurawiki/tiktoken-rs/tree/main/examples) directory in the repository.

# Usage

1. Install this tool locally with `cargo`

```sh
cargo add tiktoken-rs
```

Then in your rust code, call the API

## Counting token length

```rust
use tiktoken_rs::p50k_base;

let bpe = p50k_base().unwrap();
let tokens = bpe.encode_with_special_tokens(
  "This is a sentence   with spaces"
);
println!("Token count: {}", tokens.len());
```

## Counting max_tokens for a chat completion request

```rust
use tiktoken_rs::get_chat_completion_max_tokens;
use async_openai::types::{ChatCompletionRequestMessageArgs, Role};

let messages = vec![
    ChatCompletionRequestMessageArgs::default()
        .content("You are a helpful assistant!")
        .role(Role::System)
        .build()
        .unwrap(),
    ChatCompletionRequestMessageArgs::default()
        .content("Hello, how are you?")
        .role(Role::User)
        .build()
        .unwrap(),
];
let max_tokens = get_chat_completion_max_tokens("gpt-4", &messages).unwrap();
println!("max_tokens: {}", max_tokens);
```

`tiktoken` supports these encodings used by OpenAI models:

| Encoding name           | OpenAI models                                                             |
| ----------------------- | ------------------------------------------------------------------------- |
| `cl100k_base`           | ChatGPT models, `text-embedding-ada-002`                                  |
| `p50k_base`             | Code models, `text-davinci-002`, `text-davinci-003`                       |
| `p50k_edit`             | Use for edit models like `text-davinci-edit-001`, `code-davinci-edit-001` |
| `r50k_base` (or `gpt2`) | GPT-3 models like `davinci`                                               |

See the [examples](./examples/) in the repo for use cases. For more context on the different tokenizers, see the [OpenAI Cookbook](https://github.com/openai/openai-cookbook/blob/66b988407d8d13cad5060a881dc8c892141f2d5c/examples/How_to_count_tokens_with_tiktoken.ipynb)

# Encountered any bugs?

If you encounter any bugs or have any suggestions for improvements, please open an issue on the repository.

# Acknowledgements

Thanks @spolu for the original code, and `.tiktoken` files.

# License

This project is licensed under the [MIT License](./LICENSE).
