# Gontainer

This is container library for dependency injection implementation. This library is enhanced version of https://github.com/facebookarchive/inject

## Feature

- Register object to container (reusable)
- Check readiness for every registered oject
- Inject registered object to another object
- Get object from container

## Getting Started

### Import to your project

```bash
go get -u github.com/runsystemid/gontainer
```

## Usage

See folder _example for the usage

```go
package main

import (
	"log"
	"runsystemid/gontainer"
	"runsystemid/gontainer/example/obj"
)

var appContainer gontainer.Container

func main() {
	// Register services
	appContainer.RegisterService("sampleObject1", new(obj.SampleObject1))

	// Start up services
	if err := appContainer.Ready(); err != nil {
		log.Panic("Failed to populate service", err)
	}

	// Get registered object from container
	obj1 := appContainer.GetServiceOrNil("sampleObject1").(*obj.SampleObject1)
	obj1.Hello()

	// Initialize objects with dependencies
	obj2 := &obj.SampleObject2{}
	obj2.Object.Hello()

	appContainer.Shutdown()
}
```

## Contributing

Contributions are welcome! Please follow the [Contribution Guidelines](CONTRIBUTION.md).

## License

This project is licensed under the MIT License.
