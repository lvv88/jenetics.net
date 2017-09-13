# Jenetics for .Net

**Jenetics for .Net** is a port of the popular Genetic Algorithm framework [Jenetics](http://jenetics.io) to .NET.

## Documentation

Currently documentation is not ported but because of the nearly identical structure look into the Java Jenetics ([javadoc](http://jenetics.io/javadoc/jenetics/3.9/index.html)) and the user manual ([pdf](http://jenetics.io/manual/manual-3.9.0.pdf)).

## Requirements

### Build time
*  **.Net Core 2.0**: The [.Net Core 2.0](https://www.microsoft.com/net/download/core) SDK must be installed.

## Example

### Hello World (Ones counting)

The minimum evolution Engine setup needs a genotype factory, `Factory<Genotype<TGene>>`, and a fitness `Function`. The `Genotype` implements the `Factory` interface and can therefore be used as prototype for creating the initial `Population` and for creating new random `Genotypes`.

```cs
using System;
using System.Linq;
using Jenetics.Engine;

namespace Jenetics.Example
{
    public static class HelloWorld
    {
        // 2.) Definition of the fitness function.
        private static int Eval(Genotype<BitGene> gt)
        {
            return gt.GetChromosome().As<BitChromosome>().BitCount();
        }

        public static void Main()
        {
            // 1.) Define the genotype (factory) suitable
            //     for the problem.
            Genotype<BitGene> F()
            {
                return Genotype.Of(BitChromosome.Of(10, 0.5));
            }

            // 3.) Create the execution environment.
            var engine = Engine.Engine.Builder(Eval, F).Build();

            // 4.) Start the execution (evolution) and
            //     collect the result.
            var result = engine.Stream().Take(100).ToBestGenotype();

            Console.WriteLine("Hello World:\n" + result);
        }
    }
}
```

## License

The library is licensed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

	Copyright 2007-2017 Franz Wilhelmstötter

	Licensed under the Apache License, Version 2.0 (the "License");
	you may not use this file except in compliance with the License.
	You may obtain a copy of the License at

	http://www.apache.org/licenses/LICENSE-2.0

	Unless required by applicable law or agreed to in writing, software
	distributed under the License is distributed on an "AS IS" BASIS,
	WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	See the License for the specific language governing permissions and
	limitations under the License.
	
## Release notes
	
_[All Release Notes](RELEASE_NOTES.md)_