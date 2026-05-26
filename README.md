[update-readmes]   Mode: rewrite — migrating to template structure...
# cryptofs

[![Built with Ona](https://ona.com/build-with-ona.svg)](https://app.ona.com/#https://github.com/Interested-Deving-1896/cryptofs)

<!-- AI:start:what-it-does -->
_Description pending._
<!-- AI:end:what-it-does -->

## Architecture

<!-- AI:start:architecture -->
_Architecture documentation pending._
<!-- AI:end:architecture -->

## Install

<!-- Add installation instructions here. This section is yours — the AI will not modify it. -->

```bash
git clone https://github.com/Interested-Deving-1896/cryptofs.git
cd cryptofs
```

## Usage


### Vault Initialization

```java
Path storageLocation = Paths.get("/home/cryptobot/vault");
Files.createDirectories(storageLocation);
Masterkey masterkey = Masterkey.generate(csprng));
MasterkeyLoader loader = ignoredUri -> masterkey.copy(); //create a copy because the key handed over to init() method will be destroyed
CryptoFileSystemProperties fsProps = CryptoFileSystemProperties.cryptoFileSystemProperties().withKeyLoader(loader).build();
CryptoFileSystemProvider.initialize(storageLocation, fsProps, "myKeyId");
```

The key material used for initialization and later de- & encryption is given by the [org.cryptomator.cryptolib.api.Masterkeyloader](https://github.com/cryptomator/cryptolib/blob/2.1.2/src/main/java/org/cryptomator/cryptolib/api/MasterkeyLoader.java) interface.

### Obtaining a FileSystem Instance

You have the option to use the convenience method `CryptoFileSystemProvider#newFileSystem` as follows:  

```java
FileSystem fileSystem = CryptoFileSystemProvider.newFileSystem(
	storageLocation,
	CryptoFileSystemProperties.cryptoFileSystemProperties()
		.withKeyLoader(ignoredUri -> masterkey.copy())
		.withFlags(FileSystemFlags.READONLY) // readonly flag is optional of course
		.build());
```

or to use one of the standard methods from `FileSystems#newFileSystem`:

```java
URI uri = CryptoFileSystemUri.create(storageLocation);
FileSystem fileSystem = FileSystems.newFileSystem(
		uri,
		CryptoFileSystemProperties.cryptoFileSystemProperties()
            .withKeyLoader(ignoredUri -> masterkey.copy())
			.withFlags(FileSystemFlags.READONLY) // readonly flag is optional of course
			.build());
```

**Note:** Instead of `CryptoFileSystemProperties`, you can always pass in a `java.util.Map` with entries set accordingly.

For more details on construction, have a look at the javadoc of `CryptoFileSytemProvider`, `CryptoFileSytemProperties`, and `CryptoFileSytemUris`.

### Using the Constructed FileSystem

```java
try (FileSystem fileSystem = ...) { // see above

	// obtain a path to a test file
	Path testFile = fileSystem.getPath("/foo/bar/test");

	// create all parent directories
	Files.createDirectories(testFile.getParent());

	// Write data to the file
	Files.write(testFile, "test".getBytes());

	// List all files present in a directory
	try (Stream<Path> listing = Files.list(testFile.getParent())) {
		listing.forEach(System.out::println);
	}

}
```

For more details on how to use the constructed `FileSystem`, you may consult the [javadocs of the `java.nio.file` package](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/nio/file/package-summary.html).

## Configuration

<!-- Document configuration options here. This section is yours — the AI will not modify it. -->

## CI

<!-- AI:start:ci -->
_CI documentation pending._
<!-- AI:end:ci -->

## Mirror chain

<!-- AI:start:mirror-chain -->
This repo is maintained in [`Interested-Deving-1896/cryptofs`](https://github.com/Interested-Deving-1896/cryptofs) and mirrored through:

```
Interested-Deving-1896/cryptofs  ──►  OpenOS-Project-OSP/cryptofs  ──►  OpenOS-Project-Ecosystem-OOC/cryptofs
```

Changes flow downstream automatically via the hourly mirror chain in
[`fork-sync-all`](https://github.com/Interested-Deving-1896/fork-sync-all).
Direct commits to OSP or OOC are detected and opened as PRs back to `Interested-Deving-1896`.
<!-- AI:end:mirror-chain -->

## Contributors

<!-- AI:start:contributors -->
_Contributors pending._
<!-- AI:end:contributors -->

## Origins

<!-- AI:start:origins -->
_Original project — no upstream fork._
<!-- AI:end:origins -->

## Resources

<!-- AI:start:resources -->
_No additional resource files found._
<!-- AI:end:resources -->

## License

<!-- AI:start:license -->
[AGPL-3.0](https://github.com/Interested-Deving-1896/cryptofs/blob/develop/LICENSE.txt) © 2026 [Interested-Deving-1896](https://github.com/Interested-Deving-1896)
<!-- AI:end:license -->
