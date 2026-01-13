# Makefile for multi-language LeetCode solutions
# Usage: make <target>

.DEFAULT_GOAL := help

.PHONY: help test test-python test-js test-cpp clean

help: ## Show this help message
	@echo "Available commands:"
	@grep -E '^[a-zA-Z_-]+:.*?## .*$$' $(MAKEFILE_LIST) | sort | awk 'BEGIN {FS = ":.*?## "}; {printf "\033[36m%-20s\033[0m %s\n", $$1, $$2}'

# === Testing ===

test: test-python test-js test-cpp ## Run tests for all languages

test-python: ## Run Python tests (using pytest or simple runner)
	@for dir in problems/*/*/python; do \
		if [ -d "$$dir" ]; then \
			echo "Testing Python: $$dir"; \
			python -m unittest discover -s "$$dir" -p "solution*.py" || exit 1; \
		fi \
	done
	@echo "All Python tests passed!"

test-js: ## Run JavaScript tests (using Node.js built-in or Jest if installed)
	@for dir in problems/*/*/js; do \
		if [ -d "$$dir" ]; then \
			echo "Testing JS: $$dir"; \
			node "$$dir/solution.js" || exit 1; \
		fi \
	done
	@echo "All JS tests passed! (add Jest for real unit tests)"

test-cpp: ## Compile and run C++ solutions (simple stdin/stdout style)
	@for dir in problems/*/*/cpp; do \
		if [ -d "$$dir" ]; then \
			echo "Testing C++: $$dir"; \
			g++ -std=c++17 -Wall "$$dir/solution.cpp" -o "$$dir/a.out" && \
			"$$dir/a.out" || exit 1; \
			rm -f "$$dir/a.out"; \
		fi \
	done
	@echo "All C++ tests passed!"

# === Other useful targets ===

clean: ## Clean up build artifacts
	find . -name "*.out" -delete
	find . -name "__pycache__" -type d -exec rm -rf {} +
	rm -rf node_modules  # if using npm

# Add more: lint, format, etc.