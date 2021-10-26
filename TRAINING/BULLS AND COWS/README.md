#define MIN(X, Y) (((X) < (Y)) ? (X) : (Y))

char * getHint(char * secret, char * guess){
  int  SRecord[10] = {0};
  int  GRecord[10] = {0};
  char *Result;
  int  ACount;
  int  BCount;
  int  TotalCount;
  int  Index;

  ACount     = 0;
  for (Index = 0; secret[Index] != '\0'; Index++) {
    if (secret[Index] == guess[Index]) {
      ACount++;
    }
    SRecord[secret[Index] - '0']++;
    GRecord[guess[Index]  - '0']++;
  }

  TotalCount = 0;
  for (Index = 0; Index < 10; Index++) {
    TotalCount += MIN (SRecord[Index], GRecord[Index]);
  }
  BCount = TotalCount - ACount;

  Result = calloc (20, sizeof (char));
  sprintf (Result, "%dA%dB", ACount, BCount);

  return Result;
}
