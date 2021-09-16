# actions-set-text-output

A simple composite actions to set the job output while maintaining the text format e.g. markdown format.

[![test](https://github.com/howijd/actions-set-text-output/actions/workflows/test.yml/badge.svg)](https://github.com/howijd/actions-set-text-output/actions/workflows/test.yml)


```yml
test-usage:
  runs-on: ubuntu-latest
  outputs:
    content: ${{ steps.content.outputs.value }}
  steps:
    - name: "test simple"
      uses: howijd/actions-set-text-output@main
      id: content
      with:
        text: |
          # Set text output

          A simple composite actions to set the job output while maintaining the text format e.g. markdown format.
test-result:
  runs-on: ubuntu-latest
  needs: test-usage
  if: always()
  steps:
    - if: startsWith(needs.test-usage.outputs.content, '# Set text output')
      run: exit 0
    - if: ${{ !startsWith(needs.test-usage.outputs.content, '# Set text output') }}
      run: exit 1          
```