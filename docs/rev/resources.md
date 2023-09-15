# Resources/Tools

The following is a hastily put-together list of relevant tools and resources.

- [C++ Python bytecode disassembler](https://github.com/zrax/pycdc)
- [debugger.lua](https://github.com/slembcke/debugger.lua) - debugger for lua 
- [ShellStorm Assembler/Disassembler](https://shell-storm.org/online/Online-Assembler-and-Disassembler/) - assembly/disassembly of shellcode
- [Deobfuscating powershell](https://www.cynet.com/attack-techniques-hands-on/powershell-obfuscation-demystified-series-chapter-2-concatenation-and-base64-encoding/)
- [PSDecode](https://github.com/R3MRUM/PSDecode) - script for deobfuscating PowerShell scripts
- [movfuscator](https://github.com/xoreaxeaxeax/movfuscator/)

- Silly angr script:

```python
import angr
import sys

def main(argv):
  path_to_binary = "./three"
  project = angr.Project(path_to_binary)
  initial_state = project.factory.entry_state()
  sm = project.factory.simgr(initial_state)
  sm.explore(find=[], avoid=[])  
  for state in sm.deadended:
    print(state.posix.dumps(sys.stdin.fileno()))
  else:
    raise Exception('Could not find the solution')

if __name__ == '__main__':
  main(sys.argv)
```
