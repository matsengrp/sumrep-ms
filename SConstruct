from SCons.Script import VariantDir, Environment, Builder, Depends, Flatten
import os

VariantDir('_build', src_dir='.')

env = Environment(ENV=os.environ)
env['BUILDERS']['Latexdiff'] = Builder(action = 'latexdiff $SOURCES > $TARGET')

tmpl, = env.PDF(target='_build/tmpl.pdf',source='tmpl.tex')
#tmpl_supp, = env.PDF(target='_build/tmpl_supp.pdf', source='tmpl_supp.tex')
Default([tmpl])

#env.Latexdiff(target='diff.tex',source=['stored_tmpl.tex','tmpl.tex'])
#diff = env.PDF(target='diff.pdf',source='diff.tex')

Depends(Flatten([tmpl]),
        Flatten(['tmpl.bib'])) #, 'defs.tex'

#Depends(tmpl, tmpl_supp)

cont_build = env.Command('.continuous', ['tmpl.bib', 'tmpl.tex'],
    'while :; do inotifywait -e modify $SOURCES; scons -Q; done')
Alias('continuous', cont_build)
