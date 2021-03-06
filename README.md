# generate-contract-interface

![nodejs](https://github.com/sambacha/solidity-abstract-generator/workflows/nodejs/badge.svg)

> Generates an abstract contract in Solidity from a given contract.

## Install

```bash
$ npm install --save generate-contract-interface
```

## CLI Usage

```bash
$ generate-contract-interface < MyContract.sol
```

It does support inheritance, although it currently only works if you are doing one contract per file. You may specify a root directory for imports if it is different from the current working directory:

```bash
$ generate-contract-interface --importRoot ./contracts < MyContract.sol
```

MyContract.sol

```solidity
import './B.sol';

contract A is B {
  function a() {
  }
}
```

B.sol

```solidity
contract B {
  function b() {
  }
}
```

Output

```solidity
contract IA {
  function b();
  function a();
}
```

## API Usage



```javascript
const generateInterface = require("generate-contract-interface");

const src = `contract MyContract {
  function foo(uint a) constant public returns(uint) {
    return 0;
  }

  function bar(uint a, uint b) {
  }
}`;

console.log(generateInterface(src));
```

### API Artifacts

```solidity
/// @dev GeneratedOutput

contract IMyContract {
  function foo(uint a) constant public returns(uint);
  function bar(uint a, uint b);
}

```


## Roadmap

The following are known issues and great opportunities to make an open source contribution:

- Does not handle multiple contracts per file.
- Duplicates methods shadowing inherited methods.
- Does not output multiple levels of inheritance properly.

## License

Original Work:
ISC  [Raine Revere](https://github.com/raineorshine)
