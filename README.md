# PHP RFC: Addition of the 'static' class type.

## Introduction:
In PHP, there is the ability to make classes that have mix of static and non-static code, which can be mutable. 

The purpose of this RFC is to propose a class type of 'static', which would stateless, immutable and locked down to static functionality and types only. 

* Pros:
    * Creates the ability to be more strict in the separation of concerns.

* Cons:
    * Already somewhat achievable if you apply the discipline of proper naming conventions / directory structure to classes that only use static functionality and types.

## Use cases:
Utility classes.

## Proposed usage / Syntax:
    static class MyStaticClass
    {
        public    const FOO = 'foo';
        protected const BAR = 'bar';
        private   const BAZ = 'baz';

        public    $a;
        protected $b;
        private   $c;

        public function pubFunction(): array
        {
            return self::proFunction();
        }

        protected function proFunction(): array
        {
            return self::privFunction();
        }

        private function privFunction(): array
        {
            return [
                self::FOO,
                self::BAR,
                self::BAZ,
                self::$a,
                self::$b,
                self::$c
            ];
        }
    }

    $a = Acme\MyStaticClass::pubFunction();

## Warning / Errors / Exceptions:
    $a = new Acme\MyStaticClass;
    // This should throw ErrorException with message 'static class {className} is not initializable.'
    
    Rest should follow normal class warning / errors / exceptions.
   