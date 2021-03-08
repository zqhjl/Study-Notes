- {: id="20210308193728-zbiiux6"}
  ```java
  private static class CharacterCache {
      private CharacterCache(){}

      static final Character cache[] = new Character[127 + 1];
      static {
          for (int i = 0; i < cache.length; i++)
              cache[i] = new Character((char)i);
      }
  }
  ```
  {: id="20210308193728-eln0mjf" updated="20210308193732"}
{: id="20210308193553-g7ltboa" updated="20210308193728"}


{: id="20210301233948-5ib86kr" type="doc"}
