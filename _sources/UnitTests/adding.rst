..  Copyright (C)  Mark Guzdial, Barbara Ericson, Briana Morrison
    Permission is granted to copy, distribute and/or modify this document
    under the terms of the GNU Free Documentation License, Version 1.3 or
    any later version published by the Free Software Foundation; with
    Invariant Sections being Forward, Prefaces, and Contributor List,
    no Front-Cover Texts, and no Back-Cover Texts.  A copy of the license
    is included in the section entitled "GNU Free Documentation License".

..  shortname:: Chapter: What You Can Do with a Computer
..  description:: Some tidbits of what you can do with a computer


.. |runbutton| image:: Figures/run-button.png
    :height: 20px
    :align: top
    :alt: run button


Unit Tests
====================


Let's Run the code below (Note: one test fails just for a demonstration):


.. datafile:: TestEngine.java
  :hide:

  import java.util.ArrayList;
  import java.util.Arrays;
  import java.text.DecimalFormat;

  public class TestEngine {
      private ArrayList<String[]> tests;
      private int successes;
      public TestEngine() {
          tests = new ArrayList<>();
          successes = 0;
      }
      public <T> void assertEquals(T actual, T expected, String testName) {
          String success = "false";
          if(expected.equals(actual)) {
              success = "true";
              successes++;
          }
          String[] s = {testName, expected.toString(), actual.toString(), success};
          tests.add(s);
      }

      public <T> void assertNotEquals(T actual, T expected, String testName) {
          String success = "false";
          if(!expected.equals(actual)) {
              success = "true";
              successes++;
          }
          String[] s = {testName, expected.toString(), actual.toString(), success};
          tests.add(s);
      }

      public void assertTrue(boolean actual, String testName) {
          String success = "false";
          if (actual) {
              success = "true";
              successes++;
          }
          String[] s = {testName, "true", actual + "", success};
          tests.add(s);
      }

      public void assertFalse(boolean actual, String testName) {
          String success = "false";
          if (!actual) {
              success = "true";
              successes++;
          }
          String[] s = {testName, "False", actual + "", success};
          tests.add(s);
      }

      public <T> void assertNull(T actual, String testName) {
          String success = "false";
          String as = "null";
          if (actual == null) {
              success = "true";
              successes++;
          } else {
              as = actual.hashCode() + "";
          }
          String[] s = {testName, "null", as, success};
          tests.add(s);
      }

      public <T> void assertNotNull(T actual, String testName) {
          String success = "false";
          String as = "null";
          if (actual != null) {
              success = "true";
              successes++;
              as = actual.hashCode() + "";
          }
          String[] s = {testName, "!null", as, success};
          tests.add(s);
      }

      public <T> void assertArrayEquals(T[] actual, T[] expected, String testName) {
          String success = "false";
          if(actual.length == expected.length) {
              success = "true";
              successes++;
              for(int i = 0; i < actual.length; i++) {
                  if(!actual[i].equals(expected[i])) {
                      success = "false";
                      successes--;
                      i = actual.length;
                  }
              }
          }

          String[] s = {testName, Arrays.toString(expected), Arrays.toString(actual), success};
          tests.add(s);
      }

      public void assertArrayEquals(int[] actual, int[] expected, String testName) {
          String success = "false";
          if(actual.length == expected.length) {
              success = "true";
              successes++;
              for(int i = 0; i < actual.length; i++) {
                  if(actual[i] != (expected[i])) {
                      success = "false";
                      successes--;
                      i = actual.length;
                  }
              }
          }

          String[] s = {testName, Arrays.toString(expected), Arrays.toString(actual), success};
          tests.add(s);
      }

      public void assertArrayEquals(double[] actual, double[] expected, String testName) {
          String success = "false";
          if(actual.length == expected.length) {
              success = "true";
              successes++;
              for(int i = 0; i < actual.length; i++) {
                  if(actual[i] != expected[i]) {
                      success = "false";
                      successes--;
                      i = actual.length;
                  }
              }
          }

          String[] s = {testName, Arrays.toString(expected), Arrays.toString(actual), success};
          tests.add(s);
      }

      public void assertArrayEquals(char[] actual, char[] expected, String testName) {
          String success = "false";
          if(actual.length == expected.length) {
              success = "true";
              successes++;
              for(int i = 0; i < actual.length; i++) {
                  if(actual[i] != (expected[i])) {
                      success = "false";
                      successes--;
                      i = actual.length;
                  }
              }
          }

          String[] s = {testName, Arrays.toString(expected), Arrays.toString(actual), success};
          tests.add(s);
      }

      public void assertArrayEquals(boolean[] actual, boolean[] expected, String testName) {
          String success = "false";
          if(actual.length == expected.length) {
              success = "true";
              successes++;
              for(int i = 0; i < actual.length; i++) {
                  if(actual[i] != expected[i]) {
                      success = "false";
                      successes--;
                      i = actual.length;
                  }
              }
          }

          String[] s = {testName, Arrays.toString(expected), Arrays.toString(actual), success};
          tests.add(s);
      }
      // Only prints correct object if hashCode isnt overwritten
      public <T> void assertSame(T actual, T expected, String testName) {
          String success = "false";
          if(expected == actual) {
              success = "true";
              successes++;
          }
          String[] s = {testName, expected.hashCode() + "", actual.hashCode() + "", success};
          tests.add(s);
      }

      // Only prints correct object if hashCode isnt overwritten
      public <T> void assertNotSame(T actual, T expected, String testName) {
          String success = "false";
          if(expected != actual) {
              success = "true";
              successes++;
          }
          String[] s = {testName, expected.hashCode() + "", actual.hashCode() + "", success};
          tests.add(s);
      }

      public String run() {
          String result = "";
          result += "<table style='border: 1px solid black'><tr><th style='border: 1px solid black; text-align: center'>Result</th><th style='border: 1px solid black; text-align: center'>Actual</th><th style='border: 1px solid black; text-align: center'>Expected</th><th style='border: 1px solid black;  text-align: center'>Name</th></tr>";

          for (String[] t: this.tests) {

              if(t[3].equals("true")) {
                  result += "<tr><td bgcolor='#87d184' style='border: 1px solid black; text-align: center'>Pass</td>";
              } else {
                  result += "<tr><td bgcolor='#dc8f95' style='border: 1px solid black; text-align: center'>Fail</td>";
              }
              result += "<td style='border: 1px solid black; text-align: center'>" + t[2] +"</td><td style='border: 1px solid black; text-align: center'>"+ t[1] +"</td><td style='border: 1px solid black; text-align: center'>"+t[0]+"</td></tr>";

          }

          result += "</table>";
          double percent = (this.successes)/(1.0*this.tests.size()) * 100.0;
          result += new DecimalFormat("#.##").format(percent) + "% Passed (" + this.successes + "/" + this.tests.size() +")";
          return result;
      }
    }


.. activecode:: Add
   :language: java
   :datafile: TestEngine.java

   class Add {

       public static int add(int a, int b) {
           return a + b;
       }

   }
     =====
     public class Tester {
         public static void main(String args[]) {
             TestEngine tester = new TestEngine();
             tester.assertEquals(Add.add(2,3), 5,  "Basic");
             tester.assertEquals(Add.add(2,-3), -1, "Negative");
             tester.assertEquals(Add.add(8,3), 5,  "Special");

             System.out.println(tester.run());
         }
     }
