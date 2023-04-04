Software version: HDF5 V1.14.0
OS: Ubuntu 18.04.6 LTS
Compiler:clang

</p>

#### Build Steps:

```
./configure --disable-shared --enable-static-exec && make
```

#### Build options: None needed besides default
<p>
None needed besides default
</p>

#### Command or corpus

<p>
(https://github.com/HDFGroup/hdf5/files/11105404/poc.zip)
</p>

```
 ~/hdf5-1.14.0/in/plain_model.h5
```


#### Stack Trace:

```
Starting program: /root/hdf5-1.14.0/tools/src/h5diff/h5diff /root/hdf5-1.14.0/in/plain_model.h5 /root/hdf5-1.14.0/out/fuzz00/crashes/id:000025,sig:11,src:000000,op:flip1,pos:3977
Program received signal SIGSEGV, Segmentation fault.
0x000000000061c617 in H5HG_read (f=<optimized out>, hobj=<optimized out>, object=0xee5ca8, 
    buf_size=<optimized out>) at H5HG.c:611
611         if (heap->obj[0].begin) {
(gdb) bt
#0  0x000000000061c617 in H5HG_read (f=<optimized out>, hobj=<optimized out>, object=0xee5ca8, 
    buf_size=<optimized out>) at H5HG.c:611
#1  0x000000000095a5df in H5VL__native_blob_get (obj=0xec95a0, blob_id=<optimized out>, buf=0xee5ca8, 
    size=11, ctx=<optimized out>) at H5VLnative_blob.c:124
#2  0x000000000094bcc1 in H5VL__blob_get (obj=<optimized out>, cls=<optimized out>, blob_id=<optimized out>, 
    buf=<optimized out>, size=<optimized out>, ctx=<optimized out>) at H5VLcallback.c:7369
#3  H5VL_blob_get (vol_obj=<optimized out>, blob_id=0xef4893, buf=0x800b, size=15646640, ctx=0x201)
    at H5VLcallback.c:7398
#4  0x000000000092bdb5 in H5T__vlen_disk_read (file=0xeedcb3, _vl=<optimized out>, buf=0x800b, len=15646640)
    at H5Tvlen.c:896
#5  0x00000000007de5eb in H5T__conv_vlen (src_id=<optimized out>, dst_id=<optimized out>, 
    cdata=<optimized out>, nelmts=<optimized out>, buf_stride=<optimized out>, bkg_stride=<optimized out>, 
    buf=<optimized out>, bkg=<optimized out>) at H5Tconv.c:3343
#6  0x00000000007bf420 in H5T_convert (tpath=0x0, src_id=216172782113784218, dst_id=216172782113784219, 
    nelmts=15646640, buf_stride=513, bkg_stride=0, buf=<optimized out>, bkg=<optimized out>) at H5T.c:5449
#7  0x0000000000489e97 in H5A__read (attr=<optimized out>, mem_type=<optimized out>, buf=<optimized out>)
    at H5Aint.c:773
#8  0x0000000000958a63 in H5VL__native_attr_read (attr=0xef8e30, dtype_id=<optimized out>, buf=0xf00760, 
    dxpl_id=<optimized out>, req=<optimized out>) at H5VLnative_attr.c:202
#9  0x000000000093421e in H5VL__attr_read (obj=<optimized out>, cls=<optimized out>, 
    mem_type_id=<optimized out>, buf=<optimized out>, dxpl_id=<optimized out>, req=<optimized out>)
    at H5VLcallback.c:1204
#10 H5VL_attr_read (vol_obj=0xee1ab0, mem_type_id=216172782113784215, buf=0xf00760, 
    dxpl_id=792633534417207304, req=0x0) at H5VLcallback.c:1235
#11 0x000000000047f305 in H5A__read_api_common (attr_id=504403158265495595, dtype_id=216172782113784215, 
    buf=0xf00760, token_ptr=0x0, _vol_obj_ptr=<optimized out>) at H5A.c:1010
#12 0x000000000047f071 in H5Aread (attr_id=504403158265495595, dtype_id=216172782113784215, buf=0xf00760)
    at H5A.c:1042
#13 0x0000000000449fdb in diff_attr_data (attr1_id=504403158265495594, attr2_id=504403158265495595, 
    name1=<optimized out>, name2=<optimized out>, path1=<optimized out>, path2=<optimized out>, 
    opts=<optimized out>) at h5diff_attr.c:458
#14 0x000000000044bfd4 in diff_attr (loc1_id=<optimized out>, loc2_id=<optimized out>, path1=<optimized out>, 
    path2=<optimized out>, opts=<optimized out>) at h5diff_attr.c:658
#15 0x000000000044477e in diff (file1_id=<optimized out>, path1=<optimized out>, file2_id=<optimized out>, 
    path2=<optimized out>, opts=<optimized out>, argdata=<optimized out>) at h5diff.c:1803
#16 0x00000000004433fc in diff_match (file1_id=<optimized out>, grp1=<optimized out>, info1=<optimized out>, 
    file2_id=<optimized out>, grp2=<optimized out>, info2=<optimized out>, table=<optimized out>, 
    opts=<optimized out>) at h5diff.c:1238
---Type <return> to continue, or q <return> to quit---
#17 0x0000000000441b2d in h5diff (fname1=<optimized out>, fname2=<optimized out>, objname1=<optimized out>, 
    objname2=<optimized out>, opts=0x7fffffffdb90) at h5diff.c:1047
#18 0x0000000000400d47 in main (argc=<optimized out>, argv=<optimized out>) at h5diff_main.c:98
```
