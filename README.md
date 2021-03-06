# rspec-unit

Test::Unit compatibility for Rspec.

Just add this to your code:

    require 'rspec/unit'

and then you can write test classes like this:

    class FooTest < Rspec::Unit::TestCase
      def test_foo
        assert_equal 3, Foo::major_version
      end
    end

Using the `test_info` method, you can attach metadata to the next
defined test (this works much the same way Rake's `desc` method
attaches a description string to the next defined task):

    test_info :speed => 'slow', :run => 'nightly'
    def test_tarantula_multipass
      # ...
    end
    
You can also attach metadata to the entire class with the
`test_case_info` method:

    class BarTest < Rspec::Unit::TestCase
      test_case_info :integration => true
      
      # ...
    end

Each instance of `Rspec::Unit::TestCase` is equivalent to an
Rspec `describe` block, so it can also include `it` blocks,
`before` and `after` blocks, and nested `describe` blocks.  Test
methods and `it` blocks can contain either assertions or `should`
expressions.  `test` blocks (as found in Rails 2.x) also work.

Additionally, assertions can be used inside ordinary Rspec
examples.

## Rationale

I originally wrote test/unit compatibility for Micronaut, a lightweight
Rspec clone by Chad Humphries.  Micronaut has been rolled into Rspec as
the core of Rspec 2, and I was able to move the test/unit compatibility
over with minimal changes.

The point of this gem is not that I think test/unit is a better way
to write tests than the Rspec style.  I admit that I'm a TDD oldtimer
who sees Rspec as mostly a cosmetic (rather than fundamental) change,
but that doesn't mean it's not an important change.  My curmudgeonly
nature has its limits, and I do find specs a big improvement.

So why rspec-unit?  Three reasons:

1. I wanted to show off the generality of Micronaut's (and now Rspec's)
   architecture.  I hope rspec-unit can
   serve as an example for anyone who wants to experiment with new
   ways of expressing tests and specs on top of Rspec.
2. Many projects with existing test/unit test suites might want to
   benefit from the [metadata goodness][metadata] in Rspec 2, or begin
   a gradual, piecemeal change to an Rspec style.  That's pretty
   easy to do with rspec-unit.
3. Even when writing specs and examples, I frequently encounter
   cases where an assertion is more expressive than a `should`
   expression.  It's nice just to have assertions supported within
   Rspec examples.
      
[uth]: http://blog.thinkrelevance.com/2009/4/1/micronaut-innovation-under-the-hood
[metadata]: http://blog.thinkrelevance.com/2009/3/26/introducing-micronaut-a-lightweight-bdd-framework

## To Do

It would be nice to try using the assertion code from minitest,
which is much more compact and seems less coupled than that from
test/unit.

### Copyright

Copyright (c) 2009, 2010 Glenn Vanderburg. See LICENSE for details.
