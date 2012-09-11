# Visual Studio Testing Shim

For cross-compiling unit tests that use the 
Microsoft.VisualStudio.TestTools.UnitTesting namespace so they run with NUnit.

This project effectively aliases NUnit's attributes so they are named like
Microsoft's attributes.  It uses inheritance to accomplish the aliasing
so that you can avoid type aliases and preprocessor directives.

	namespace Microsoft.VisualStudio.TestTools.UnitTesting
	{
	    public class TestClassAttribute : NUnit.Framework.TestFixtureAttribute {}
	}

Thus you may cross-compile a single unit test source file similar to this one:

	using FluentAssertions;
	using Microsoft.VisualStudio.TestTools.UnitTesting;

	namespace MyTests
	{
	    [TestClass]
	    public class MyTest
	    {
	        [TestMethod]
	        public void Canary()
	        {
            	var subject = new object();
	            subject.Should().NotBeNull();
	        }
	    }
	}
	
You may cross-compile it to run with either Visual Studio / MSTest or 
an NUnit test runner (such as with MonoDevelop). 
In the project that references **NUnit.Framework**, simply add a reference to 
**VisualStudioTestingShim**.

For MonoTouch users you may reference **VisualStudioTestingShim.MonoTouch** 
along with **MonoTouch.NUnitLite**.
