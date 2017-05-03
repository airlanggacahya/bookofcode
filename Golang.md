
# Golang

## Function Name
TODO

## Variable Name
TODO

## Package Name
TODO

## New Line Ending
New Line is TODO

## Indentation
Source code identation is using TAB. Please read Automatic Formating.

## Automatic Formating
Please use go fmt for formating source code before commit into repository.
Even better, use golang plugin for your favourite text editor for automatic formating every file save.

## Global Variable
Do Not Use Global Variable. It's recommeded to pass variable using Context or similar technique.

## Error Handling

### Library
Please return error handling on your function. Delegate error handling to your caller. DO NOT IGNORE ERROR. In most case, your caller need to detect error and react accordingly.

Use error as last variable on your return value.

```go
func ParseSomething(val string) (type string, value int, error) {
    // call function that return error
    err := ProbablyError(val)
    if err != nil {
        // throw error
        return "", 0, err
    }
    // return without error
    return "OVERDRIVE", 0, nil
}
```

### Application
If you are wrapping library error, then create your own Error variable on global level and then use them.

```go
var ErrorSaveFailed = errors.New("Error Save Failed")

func SaveFile(val string) error {
    err := OperationMayError(val)
    if err != nil {
        return ErrorSaveFailed
    }

    return nil
}
```

On the caller you can compare with the var name if you need to respond based on the error code. Otherwise, handle like the usual.

```go
func SaveFileCaller(val string) error {
    err := SaveFile(val)
    if err == ErrorSaveFailed {
        // Handle special for  Save Failed
        return err
    } else if err != nil {
        // Handle for other error
        return err
    }

    // No error here
}
```

This pattern may obscure real error.
