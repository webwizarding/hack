# Shitty CTF challenge 

`https://tryhackme.com/r/room/nsacrptograpghychallenge`

Deleted by author because he knows its bad and doesn't know anything about CTF challenges.

---

## Challenge
```
Good luck
it also has a riddle in it. >:)
Hint: you have to shift the encode message into any number, so you have to guess the shift number. when you guess it right, you'll decode it and analyze the riddle and what this riddle is saying
The riddle only has one word to say, if you put mutiple words. You're incorrect, so good luck 
```

---
### Provided files

```
N xzpjn rtyux ymjw f rwjfxy fsi mjfw fqi gfqxy ymj fwyn. N mfq st nx htqif, gjw N htzr fqjqi bnymjw dj ymnx fsis.
```

---

## Solving
`Cipher decoder script`
```python
def caesar_cipher_decrypt(ciphertext, shift):
    decrypted_text = ""
    for char in ciphertext:
        if char.isalpha():  
            shifted_char = chr(((ord(char.lower()) - 97 - shift) % 26) + 97)

            if char.isupper():
                decrypted_text += shifted_char.upper()
            else:
                decrypted_text += shifted_char
        else:
            decrypted_text += char
    return decrypted_text

encrypted_riddle = "N xzpjn rtyux ymjw f rwjfxy fsi mjfw fqi gfqxy ymj fwyn. N mfq st nx htqif, gjw N htzr fqjqi bnymjw dj ymnx fsis."

for shift in range(1, 26):
    decrypted_message = caesar_cipher_decrypt(encrypted_riddle, shift)
    print(f"Shift {shift}: {decrypted_message}")
```

--- 

`Shift text output`
```
Shift 1: M wyoim qsxtw xliv e qviewx erh liev eph fepwx xli evxm. M lep rs mw gsphe, fiv M gsyq epiph amxliv ci xlmw erhr.
Shift 2: L vxnhl prwsv wkhu d puhdvw dqg khdu dog edovw wkh duwl. L kdo qr lv frogd, ehu L frxp dohog zlwkhu bh wklv dqgq.
Shift 3: K uwmgk oqvru vjgt c otgcuv cpf jgct cnf dcnuv vjg ctvk. K jcn pq ku eqnfc, dgt K eqwo cngnf ykvjgt ag vjku cpfp.
Shift 4: J tvlfj npuqt uifs b nsfbtu boe ifbs bme cbmtu uif bsuj. J ibm op jt dpmeb, cfs J dpvn bmfme xjuifs zf uijt boeo.
Shift 5: I sukei motps ther a mreast and hear ald balst the arti. I hal no is colda, ber I coum aleld wither ye this andn.
Shift 6: H rtjdh lnsor sgdq z lqdzrs zmc gdzq zkc azkrs sgd zqsh. H gzk mn hr bnkcz, adq H bntl zkdkc vhsgdq xd sghr zmcm.
Shift 7: G qsicg kmrnq rfcp y kpcyqr ylb fcyp yjb zyjqr rfc yprg. G fyj lm gq amjby, zcp G amsk yjcjb ugrfcp wc rfgq ylbl.
Shift 8: F prhbf jlqmp qebo x jobxpq xka ebxo xia yxipq qeb xoqf. F exi kl fp zliax, ybo F zlrj xibia tfqebo vb qefp xkak.
Shift 9: E oqgae ikplo pdan w inawop wjz dawn whz xwhop pda wnpe. E dwh jk eo ykhzw, xan E ykqi whahz sepdan ua pdeo wjzj.
Shift 10: D npfzd hjokn oczm v hmzvno viy czvm vgy wvgno ocz vmod. D cvg ij dn xjgyv, wzm D xjph vgzgy rdoczm tz ocdn viyi.
Shift 11: C moeyc ginjm nbyl u glyumn uhx byul ufx vufmn nby ulnc. C buf hi cm wifxu, vyl C wiog ufyfx qcnbyl sy nbcm uhxh.
Shift 12: B lndxb fhmil maxk t fkxtlm tgw axtk tew utelm max tkmb. B ate gh bl vhewt, uxk B vhnf texew pbmaxk rx mabl tgwg.
Shift 13: A kmcwa eglhk lzwj s ejwskl sfv zwsj sdv tsdkl lzw sjla. A zsd fg ak ugdvs, twj A ugme sdwdv oalzwj qw lzak sfvf.
Shift 14: Z jlbvz dfkgj kyvi r divrjk reu yvri rcu srcjk kyv rikz. Z yrc ef zj tfcur, svi Z tfld rcvcu nzkyvi pv kyzj reue.
Shift 15: Y ikauy cejfi jxuh q chuqij qdt xuqh qbt rqbij jxu qhjy. Y xqb de yi sebtq, ruh Y sekc qbubt myjxuh ou jxyi qdtd.
Shift 16: X hjztx bdieh iwtg p bgtphi pcs wtpg pas qpahi iwt pgix. X wpa cd xh rdasp, qtg X rdjb patas lxiwtg nt iwxh pcsc.
Shift 17: W giysw achdg hvsf o afsogh obr vsof ozr pozgh hvs ofhw. W voz bc wg qczro, psf W qcia ozszr kwhvsf ms hvwg obrb.
Shift 18: V fhxrv zbgcf gure n zernfg naq urne nyq onyfg gur negv. V uny ab vf pbyqn, ore V pbhz nyryq jvgure lr guvf naqa.
Shift 19: U egwqu yafbe ftqd m ydqmef mzp tqmd mxp nmxef ftq mdfu. U tmx za ue oaxpm, nqd U oagy mxqxp iuftqd kq ftue mzpz.
Shift 20: T dfvpt xzead espc l xcplde lyo splc lwo mlwde esp lcet. T slw yz td nzwol, mpc T nzfx lwpwo htespc jp estd lyoy.
Shift 21: S ceuos wydzc drob k wbokcd kxn rokb kvn lkvcd dro kbds. S rkv xy sc myvnk, lob S myew kvovn gsdrob io drsc kxnx.
Shift 22: R bdtnr vxcyb cqna j vanjbc jwm qnja jum kjubc cqn jacr. R qju wx rb lxumj, kna R lxdv junum frcqna hn cqrb jwmw.
Shift 23: Q acsmq uwbxa bpmz i uzmiab ivl pmiz itl jitab bpm izbq. Q pit vw qa kwtli, jmz Q kwcu itmtl eqbpmz gm bpqa ivlv.
Shift 24: P zbrlp tvawz aoly h tylhza huk olhy hsk ihsza aol hyap. P ohs uv pz jvskh, ily P jvbt hslsk dpaoly fl aopz huku.
Shift 25: O yaqko suzvy znkx g sxkgyz gtj nkgx grj hgryz znk gxzo. O ngr tu oy iurjg, hkx O iuas grkrj coznkx ek znoy gtjt.
```

---

# Flag
After decoding the shift text output this is what we get
```
I emerge from the deep sea a beast and rise high above the sky. I am so at peace, yet I fall back down earth to die.
```

---
