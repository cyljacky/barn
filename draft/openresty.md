

# Characteristics

- Nginx + Lua
- allows for 3rd party plugins
- Fast

## Nginx Pros
- event-driven, and async non-blocking IO => high performance
- light-weight
- modular design
- multi-thread

## Why Lua?

Originally uses C, why Lua?

- Complimentary with C/C++
- lightweight scripting language(engine)
- fastest scripting language

## What can it do?
- some request access control can be written in Openresty, instead of Application, to increase performance.
- script various existing nginx C modules and Lua modules and construct extremely high-performance web applications