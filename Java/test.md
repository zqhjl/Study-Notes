- {: id="20210308193926-b47b4tf"}123456
  {: id="20210308193926-cksn7sf" updated="20210308193928"}

  ```java
  public boolean equals(Object anObject) {
      if (this == anObject) {
          return true;
      }
      if (anObject instanceof String) {
          String anotherString = (String)anObject;
          int n = value.length;
          if (n == anotherString.value.length) {
              char v1[] = value;
              char v2[] = anotherString.value;
              int i = 0;
              while (n-- != 0) {
                  if (v1[i] != v2[i])
                      return false;
                  i++;
              }
              return true;
          }
      }
      return false;
  }
  ```
  {: id="20210308193728-eln0mjf" updated="20210308193939"}
{: id="20210308193922-l3gpl99" updated="20210308193926"}


{: id="20210301233948-5ib86kr" type="doc"}
